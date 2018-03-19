Sky and Fog

In HDRP, sky and fog are setup via the interpolation volume framework (link to Volume doc?). The goal is for the user to be able to dynamically change the look of the sky and fog depending on the camera position.

We also provide the necessary tools to offer consistent baking of lightmaps and probes.

The Sky Framework used by HDRP is also designed in a way that it is easy for users to write their own custom sky and use it in their project with minimal effort.

As part of the Volume framework, all local settings components described below are actually *VolumeComponents* which need to be added to a *Volume *component on a regular *GameObject. *As such, all their parameters can be interpolated between different volumes.

# Setting up the Sky

Setting up a sky has two goals: The first one is to define what will be displayed in the background of the scene for a given camera. The second one is to define environment lighting, namely sky reflection and sky ambient probe which is then later used to render lightmaps (real-time or baked).

Settings are split between global settings which are per project/platform and local settings that use the volume framework and can change depending on the scene or camera position.

## Global Sky Settings

Global settings for the sky are in the HDRenderPipeline configuration asset:

![](../uploads/Main/Copyof Sky and Fog_image_0.png)

__Sky Reflection Size__

This parameter drives the size of the cubemap generated from the sky and used for fallback reflection when no local reflection probes are present. It has no effect on the quality of the sky rendered in the background.

__Sky Lighting Override Mask__

In some cases, users may want to dissociate lighting environment from what is rendered in the background (a typical example is to have a very dark sky at night but have a brighter lighting so that the player can still see).

In order to achieve this, users can define the sky lighting override mask which is a Layer mask. If any volumes are present in this layer then environment lighting will use these volumes instead of those from the main camera. If this mask is set to *Nothing *or if there are no volume in this mask then lighting will come from volumes setup in the main camera volume layer mask.

In practice this means that user can define two sets of masks, one for the visual sky and the other for the lighting. Both sets of volume will then be interpolated independently from each other.

Note that lighting override does not affect baked lighting.

## Local Sky Settings

Once global parameters are set, users need to setup volumes with the correct components to setup local parameters for the sky. Currently HDRP provides two different kind of skies.

__Procedural Sky__

This sky is similar to the procedural sky provided with the built-in Unity Render Pipelines. 

![](../uploads/Main/Copyof Sky and Fog_image_1.png)

| Property| Function |
|:---|:---| 
| __Enable Sun Disk__| Display sun disk |
| __Sun Size__| Size of the sun disk |
| __Sun Size Convergence__|  |
| __Atmospheric Thickness__|  |
| __Sky Tint__| Color of the sky hemisphere |
| __Ground Color__| Color of the ground hemisphere |
| __Exposure__| Exposure applied to the sky |
| __Multiplier__| Multiplier applied to the sky |
| __Update Mode__| Rate at which the sky environment (reflection en ambient probe) should be updated |
| On Changed| Sky environment is updated when one of its parameter changes |
| On Demand| Sky Environment is explicitly updated by the script |
| Realtime| Sky environment is updated regularly |
| Update Period| Period (in seconds) at which the realtime sky is updated (0 means every frame) |



__HDRI Sky__

Simple sky represented by a cubemap texture.

![](../uploads/Main/Copyof Sky and Fog_image_2.png)

| Property| Function |
|:---|:---| 
| __Hdri sky__| Cubemap representing the sky |
| __Exposure__| Exposure applied to the sky |
| __Multiplier__| Multiplier applied to the sky |
| __Rotation__| Rotation applied to the cubemap in degrees |
| __Update Mode__| Rate at which the sky environment (reflection en ambient probe) should be updated |
| On Changed| Sky environment is updated when one of its parameter changes |
| On Demand| Sky Environment is explicitly updated by the script |
| Realtime| Sky environment is updated regularly |
| Update Period| Period (in seconds) at which the realtime sky is updated (0 means every frame) |



## Baking Global Illumination with the sky

In HDRP the sky is completely controlled by the volume system. It means that in the editor, the current state of the sky will depend on the camera position. The consequence is that for users to get a consistent lighting baking, we can’t rely on what is in the scene.

Instead the sky used for baking is set explicitly by the user through the Baking Sky component.

![](../uploads/Main/Copyof Sky and Fog_image_3.png)

User should select a volume profile which contains the sky intended to be used for baking and then choose the right type (in case the profile contains different kinds of skies). If the component is added to a game object that already has a Volume, the profile property will be automatically populated with the corresponding profile asset.

This sky setting will live outside of the volume framework and thus will never be interpolated based on the camera position. Any time the baking is required, this is the sky that will be used.

Only one such component can be present in the editor at any given time. Any additional component of the same type will generate a warning and be ignored.

# Setting up the Fog

Fog is the effect of overlaying a color onto objects dependant on the distance from the camera. This is used to simulate fog or mist in outdoor environments and is also typically used to hide clipping of objects when a camera’s far clip plane has been moved forward for performance.

In HDRP, users can choose between two different kind of fogs, linear and exponential fog. All types of materials (lit or unlit) will react correctly to the fog. Depending on the type of fog, density will evolve differently with respect to distance from camera and world space height.

Instead of using a constant color, both types of fog can choose to use the background sky as a source for color. In this case, the color will be sampled from different mip maps of the cubemap generated from the current sky settings. Chosen mip will vary linearly between the blurriest one to the highest resolution one depending on the distance from camera and the "Mip Fog" parameters. Users can also choose to limit the resolution of the higher mip used.

For both types of fog, density is computed from camera distance and world space height independently and then multiplied together to obtain the final result.

__Linear Fog__

Density will increase linearly with view distance and world space height depending on the provided parameters.

![](../uploads/Main/Copyof Sky and Fog_image_4.png)

| Property| Function |
|:---|:---| 
| __Density__| Global multiplier for the fog density |
| __Color Mode__| Source of the fog color |
| Constant Color| Fog is a constant color |
| Color| Color of the fog |
| Sky Color| Fog color is sampled from the sky |
| Mip Fog Near| Distance at which the blurriest sky mip is used |
| Mip Fog Far| Distance at which the higher sky mip (see "Mip Fog Max Mip" ) is used |
| Mip Fog Max Mip| Maximum mip map used to sample the color (1.0 being highest resolution and 0.0 lowest resolution). |
| __Fog Start__| Distance from camera at which fog density starts to increase from zero. |
| __Fog End__| Distance from camera at which fog density is maximum. |
| __Fog Height Start__| Height at which fog density starts to decrease |
| __Fog Height End__| Height at which fog density is zero |



__Exponential Fog__

Density will increase exponentially with view distance and world space height depending on the provided parameters.

![](../uploads/Main/Copyof Sky and Fog_image_5.png)

| Property| Function |
|:---|:---| 
| __Density__| Global multiplier for the fog density |
| __Color Mode__| Source of the fog color |
| Constant Color| Fog is a constant color |
| Color| Color of the fog |
| Sky Color| Fog color is sampled from the sky |
| Mip Fog Near| Distance at which the blurriest sky mip is used |
| Mip Fog Far| Distance at which the higher sky mip (see "Mip Fog Max Mip" ) is used |
| Mip Fog Max Mip| Maximum mip map used to sample the color (1.0 being highest resolution and 0.0 lowest resolution). |
| __Fog Distance__| Distance from camera at will reach maximum |
| __Fog Base Height__| World space height at which fog density starts to decrease from 1.0 |
| __Fog Height Attenuation__| Fall off of height fog attenuation (bigger values will make attenuation sharper) |



# Visual Environment

Once the proper components have been setup, users need to specify what kind of sky and fog should be used for rendering. This is done through the Visual Environment component.

![](../uploads/Main/Copyof Sky and Fog_image_6.png)

| Property| Function |
|:---|:---| 
| __Sky Type__| Type of sky used for rendering. This list will be automatically updated with any custom sky written by users |
| __Fog Type__| Type of fog used for rendering |



To help setting things up more easily, users can use the contextual menu to directly create a game object named "Scene Settings" and go from there. This game object is already setup with a default procedural sky and exponential fog inside a global Volume (it also contains default shadow settings).

![](../uploads/Main/Copyof Sky and Fog_image_7.png)

# Writing Custom Sky Renderers

The sky system is setup in a way that allows users to develop their own kind of sky with their own parameters and shaders.

Three things are needed in order to write your own sky.

__SkySettings__

Create a new class that inherits from *SkySettings*. This class will contain all parameters specific to the particular sky renderer user is writing. Please refer to the Volume system documentation to learn how to declare volume parameters.

Three things are mandatory to write:

* SkyUniqueID attribute: This must be an integer unique to this particular sky. Must not clash with any other sky settings. The SkyType enum is available for users to see what values are already used by HDRP.

* GetHashCode: This is used by the sky system to determine when to re-render the sky reflection cubemap.

* CreateRenderer: This is used by the sky system to instantiate the proper renderer.

Exemple: HDRI Sky
```
 [SkyUniqueID(87248]<br/>    public class HDRISky : SkySettings
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
        public abstract void RenderSky(BuiltinSkyParameters builtinParams, bool renderForCubemap);
        // Returns true if provided sky setting parameters are valid.
        public abstract bool IsValid();
    }

```

Exemple: HDRISkyRenderer:

```
public class HDRISkyRenderer : SkyRenderer<br/>{
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

    public override void RenderSky(BuiltinSkyParameters builtinParams, bool renderForCubemap)
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

After doing all this, the new Sky should automatically appear in the combo box in the *Visual Environment* component.

