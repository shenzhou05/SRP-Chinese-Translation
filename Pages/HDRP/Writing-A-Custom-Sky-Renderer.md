# Writing A Custom Sky Renderer

The sky system is setup in a way that allows users to develop their own kind of sky with their own parameters and shaders while still keeping it consistent with the lighting pipeline.

Three things are needed in order to write your own sky.

__SkySettings__

Create a new class that inherits from *SkySettings*. This class will contain all parameters specific to the particular sky renderer user is writing. Please refer to the Volume system documentation to learn how to declare volume parameters.

Three things are mandatory to write:

* SkyUniqueID attribute: This must be an integer unique to this particular sky. Must not clash with any other sky settings. The SkyType enum is available for users to see what values are already used by HDRP.

* GetHashCode: This is used by the sky system to determine when to re-render the sky reflection cubemap.

* CreateRenderer: This is used by the sky system to instantiate the proper renderer.

Exemple: HDRI Sky

```
    [SkyUniqueID(87248)]
    public class HDRISky : SkySettings
    {
        [Tooltip("Cubemap used to render the sky.")]
        public CubemapParameter hdriSky = new CubemapParameter(null);

        public override SkyRenderer CreateRenderer()
        {
            return new HDRISkyRenderer(this);
        }
    
        public override int GetHashCode()
        {
            int hash = base.GetHashCode();
    
            unchecked
            {
                hash = hdriSky.value != null ? hash * 23 + hdriSky.GetHashCode() : hash;
            }
    
            return hash;
        }
    }
```


    

__SkyRenderer__

This is the class that will actually render the sky, either into a cubemap for lighting or on the background. This is where users must implement all their specific rendering.

It must implement this interface:

```
    public abstract class SkyRenderer
    {
        // Method used to initialize any resource for the sky rendering (shaders, …)
        public abstract void Build();
        // Method used to clean up any resource previously allocated
        public abstract void Cleanup();
        // SkyRenderer is responsible for setting up render targets provided in builtinParams
        public abstract void SetRenderTargets(BuiltinSkyParameters builtinParams);
        // renderForCubemap: When rendering into a cube map, no depth buffer is available so user has to make sure not to use depth testing or the depth texture.
        // renderSunDisk: If the sky renderer supports it, it should not render the sun disk when this value is set to false (it is used to get consistent baking)
        public abstract void RenderSky(BuiltinSkyParameters builtinParams, bool renderForCubemap, bool renderSunDisk);
        // Returns true if provided sky setting parameters are valid.
        public abstract bool IsValid();
    }

```


Exemple: HDRISkyRenderer:


```
 public class HDRISkyRenderer : SkyRenderer
 {
    Material m_SkyHDRIMaterial; // Renders a cubemap into a render texture (can be cube or 2D)
    MaterialPropertyBlock m_PropertyBlock;
    HDRISky m_HdriSkyParams;

    public HDRISkyRenderer(HDRISky hdriSkyParams)
    {
        m_HdriSkyParams = hdriSkyParams;
        m_PropertyBlock = new MaterialPropertyBlock();
    }
    
    public override void Build()
    {
        var hdrp = GraphicsSettings.renderPipelineAsset as HDRenderPipelineAsset;
        m_SkyHDRIMaterial = CoreUtils.CreateEngineMaterial(hdrp.renderPipelineResources.hdriSky);
    }
    
    public override void Cleanup()
    {
        CoreUtils.Destroy(m_SkyHDRIMaterial);
    }
    
    public override void SetRenderTargets(BuiltinSkyParameters builtinParams)
    {
        if (builtinParams.depthBuffer == BuiltinSkyParameters.nullRT)
        {
            HDUtils.SetRenderTarget(builtinParams.commandBuffer, builtinParams.hdCamera, builtinParams.colorBuffer);
        }
        else
        {
            HDUtils.SetRenderTarget(builtinParams.commandBuffer, builtinParams.hdCamera, builtinParams.colorBuffer, builtinParams.depthBuffer);
        }
    }
    
    public override void RenderSky(BuiltinSkyParameters builtinParams, bool renderForCubemap, bool renderSunDisk)
    {
        m_PropertyBlock.SetTexture(HDShaderIDs._Cubemap, m_HdriSkyParams.hdriSky);
        m_PropertyBlock.SetVector(HDShaderIDs._SkyParam, new Vector4(m_HdriSkyParams.exposure, m_HdriSkyParams.multiplier, -m_HdriSkyParams.rotation, 0.0f)); // -rotation to match Legacy...
    
        // This matrix needs to be updated at the draw call frequency.
        m_PropertyBlock.SetMatrix(HDShaderIDs._PixelCoordToViewDirWS, builtinParams.pixelCoordToViewDirMatrix);
    
        CoreUtils.DrawFullScreen(builtinParams.commandBuffer, m_SkyHDRIMaterial, m_PropertyBlock, renderForCubemap ? 0 : 1);
    }
    
    public override bool IsValid()
    {
        return m_HdriSkyParams != null && m_SkyHDRIMaterial != null;
    }
}

```


__Rendering Shader__

This is highly dependent on what the particular sky is supposed to look like. Here we’ll just show the example of HDRISky.

Note that we implemented two passes, one that uses Depth Test for rendering the sky in the background (so that it’s occluded by geometry) and the other that does not for when the sky is rendered into the reflection cubemap.


```

Shader "Hidden/HDRenderPipeline/Sky/HDRISky"<br/>{
    HLSLINCLUDE

    #pragma vertex Vert
    #pragma fragment Frag
    
    #pragma target 4.5
    #pragma only_renderers d3d11 ps4 xboxone vulkan metal
    
    #include "CoreRP/ShaderLibrary/Common.hlsl"
    #include "CoreRP/ShaderLibrary/Color.hlsl"
    #include "CoreRP/ShaderLibrary/CommonLighting.hlsl"
    
    TEXTURECUBE(_Cubemap);
    SAMPLER(sampler_Cubemap);
    
    float4   _SkyParam; // x exposure, y multiplier, z rotation
    float4x4 _PixelCoordToViewDirWS; // Actually just 3x3, but Unity can only set 4x4
    
    struct Attributes
    {
        uint vertexID : SV_VertexID;
    };
    
    struct Varyings
    {
        float4 positionCS : SV_POSITION;
    };
    
    Varyings Vert(Attributes input)
    {
        Varyings output;
        output.positionCS = GetFullScreenTriangleVertexPosition(input.vertexID, UNITY_RAW_FAR_CLIP_VALUE);
        return output;
    }
    
    float4 Frag(Varyings input) : SV_Target
    {
        // Points towards the camera
        float3 viewDirWS = normalize(mul(float3(input.positionCS.xy, 1.0), (float3x3)_PixelCoordToViewDirWS));
        // Reverse it to point into the scene
        float3 dir = -viewDirWS;
    
        // Rotate direction
        float phi = DegToRad(_SkyParam.z);
        float cosPhi, sinPhi;
        sincos(phi, sinPhi, cosPhi);
        float3 rotDirX = float3(cosPhi, 0, -sinPhi);
        float3 rotDirY = float3(sinPhi, 0, cosPhi);
        dir = float3(dot(rotDirX, dir), dir.y, dot(rotDirY, dir));
    
        float3 skyColor = ClampToFloat16Max(SAMPLE_TEXTURECUBE_LOD(_Cubemap, sampler_Cubemap, dir, 0).rgb * exp2(_SkyParam.x) * _SkyParam.y);
        return float4(skyColor, 1.0);
    }
    
    ENDHLSL
    
    SubShader
    {
        Pass
        {
            ZWrite Off
            ZTest Always
            Blend Off
            Cull Off
    
            HLSLPROGRAM
            ENDHLSL
    
        }
    
        Pass
        {
            ZWrite Off
            ZTest LEqual
            Blend Off
            Cull Off
    
            HLSLPROGRAM
            ENDHLSL
        }
    
    }
    Fallback Off
}

```

After doing all this, the new Sky should automatically appear in the combo box in the *Visual Environment *component.