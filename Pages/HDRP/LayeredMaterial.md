# Layered Material

The layered material is used to stack 2 to 4 materials on the same object. This material can be helpful to create diversity or to integrate objects between them.

The cost of this material is more heavy than a standard material, so use it when it is needed.

The layered material uses the HDRenderPipeline

# 1 Create a layered material.

First step is to create a material.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/LayeredMaterialTemp/image_0.png)

Modify shader to LayeredLit or LayeredLitTessellation. It depending if the tessellation is needed.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/LayeredMaterialTemp/image_1.png)

# 2 Layered material setting.

Shader type selection

Surface management

Tessellation management

Vertex animation

Layers management

Emissive management

Advanced Options

Material preview

Tag and asset bundle assignment

## 2.1 Surface options.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/LayeredMaterialTemp/image_2.png)

__Surface type:__ Opaque or transparent.

__Transparent options:__

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/LayeredMaterialTemp/image_3.png)

* Blend mode: Alpha (default), Additive, PremultipliedAlpha.
([https://docs.unity3d.com/Manual/SL-Blend.html](https://docs.unity3d.com/Manual/SL-Blend.html))

* Blend preserve specular lighting: Blend mode will only affect direct lighting, allowing correct specular lighting (reflection) on transparent object.

* Enable Fog: Enable fog on transparent object.

* Pre Refraction Pass: Render objects before the refraction pass.

* Transparent Sort Priority: Allow to define priority (from -100 to +100) to solve sorting issue with transparent.

__Alpha Cutoff:__ To enable alpha test (0 transparent, 1 opaque). Alpha cutoff has an handle to define the threshold between transparent and opaque.

__Double side:__ Enable double side. Normal can be set to mirror (default) or flip.

__Material type: __Standard or Subsurface Scattering and Transmission

Subsurface Scattering and Transmission type:

* Both

* SSS only

* Transmission only

__Enable Decal:__ Allow to specify if the material can receive decal or not.

__Enable MotionVector For Vertex Animation:__ This will enable an object motion vector pass for this material. Useful if wind animation is enabled or if displacement map is animated.

__Displacement mode:__

Tesselation activated:

Displacement mode:__ __none or tessellation displacement.

* __None:__ tessellation can be used only to smooth the geometry without any heightmap.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/LayeredMaterialTemp/image_4.png)

* __Tessellation displacement:__ height map is used to manage the displacement with the tessellation.

Tessellation displacement option:

* Lock with object scale: when activate the object scale keeps the height map appearance.

* Lock with height map tilling rate: the material tiling keeps the height map appearance.

Tessellation displacement example:

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/LayeredMaterialTemp/image_5.png)

Tessellation not activated:

Displacement mode: none, vertex displacement or pixel displacement.

* __None:__ do nothing.

* __Vertex displacement:__ use height map to move vertices.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/LayeredMaterialTemp/image_6.png)

Vertex displacement option:

* Lock with object scale: when activate the object scale keeps the height map appearance.

* Lock with height map tilling rate: the material tiling keeps the height map appearance.

Vertex displacement example:

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/LayeredMaterialTemp/image_7.png)

* __Pixel Displacement:__ Enable the parallax occlusion mapping. Parallax occlusion mapping can only dig base on the height map. Use it only on flat surfaces.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/LayeredMaterialTemp/image_8.png)

Pixel displacement option:

* Lock with object scale: when activate the object scale keep the height map appearance.

* Lock with height map tilling rate: the material tiling keep the height map appearance.

* Minimum steps: Minimum steps (texture sample) to use with per pixel displacement mapping.

* Maximum steps: Maximum steps (texture sample) to use with per pixel displacement mapping.

* Fading mip level start: Starting heightmap mipmap lod number where the parallax occlusion mapping effect start to disappear.

* Primitive length: let it at 1.

* Primitive width:  let it at 1.

* Enable Depth Offset: Enable depthOffset on this shader (use with heightmap).

Per pixel displacement example:

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/LayeredMaterialTemp/image_9.jpg)

## 2.2 Tessellation options.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/LayeredMaterialTemp/image_10.png)

__Tessellation Mode:__ None or Phong.

* None: Linear tessellation between two vertices,

* Phong: Smooth tessellation between two vertices.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/LayeredMaterialTemp/image_11.png)

__Tessellation factor:__ polygon division factor. Values are between 0 (original geometry) and 64.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/LayeredMaterialTemp/image_12.jpg)

__Start fade distance:__ Distance in meter where the tessellation start to reduce.

__End fade distance:__ Distance in meter where the tessellation factor is 0.

__Triangle size:__ manage polygon division compared to screen size in pixels.

__Shape factor: __Only available with phong tessellation mode. It is the__ __strength of phong tessellation shape (lerp factor between 0 and 1).

## 2.3 Vertex animation.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/LayeredMaterialTemp/image_13.png)

__Enable wind:__ Activate the wind interaction. A wind asset with the associate script should be in the scene.

__Initial Bend:__ increase or decrease the bend effect depending about the wind setting.

__Stiffness:__ increase or decrease the stiffness from bottom to top.

__Drag:__ manage the move amplitude.

__Shiver drag:__ manage the shiver amplitude. The vertex alpha modulates the amplitude.

__Shiver directionality:__ handle to manage shiver directionality between mesh normal (0) and wind direction (1).

## 2.4 Inputs.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/LayeredMaterialTemp/image_14.png)

__Layer Count:__ handle to set between 2 and 4 layers.

__Layer Mask:__ Texture to manage layers visibility. R for layer 1, G for layer 2, B for layer 3, alpha for main layer.

__BlendMask UV Mapping:__ Set the mask UV channel.

* Tiling: Mask UV tiling.

* Offset: Offset the Mask UV.

__Vertex color mode:__ use vertex color combine to layer mask to manage layers visibility.

None: vertex color unused.

Multiply: for each channel multiply the vertex color value with the mask. Default mask value is 1.

Add: for each channel middle grey (128, 128, 128) is the mask value. Other values override the mask value. 0 to 127 is used to modulate the erasure and 129 to 255 is used to modulate the add.

__Main layer influence: __allow layers 1, 2 and 3 to be influenced by the main layer. Albedo, normal and height influences can be set into each layer.

__Use Height Based blend: __activate blending via height map. 

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/LayeredMaterialTemp/image_15.jpg)

The use of height base blend allows the height blend transition to manage the layer distance transition. The unit is in world unit between 0 and 1.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/LayeredMaterialTemp/image_16.png)

__Lock layers 123 tiling with object scale: __the object scale is multiplied to the material tiling to keep the height map appearance.

__Material References:__

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/LayeredMaterialTemp/image_17.png)

It is the list of the materials used in the layered shader. If a material source has been modified, it can re-synchronize totally or without original UV mapping settings.

__Main layer:__ It is the undermost layer. It can influence upper layers with albedo, normal and height.

__Layer ____1____, ____2____, ____3____:__ They are rendered on top of the main layer. The layer 3 is rendered at last on top.

# 3 Layers.

## 3.1 Main layer.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/LayeredMaterialTemp/image_18.png)

### 3.1.1 Layering Options:

__Layer influence Mask:__ When the main layer influence is active, a mask can be add to define influence areas (white = 100%, black = 0%).

__Height Offset:__ Offset the layer without offset the geometry.

### 3.1.2 Inputs:

__Base color + opacity:__ assign the albedo texture. The texture is multiplied by the material color. If no texture is assigned, the color is the base color. Texture alpha is used as alpha.

__Metallic:__ this handle allows to set if a material is metallic or not. If a mask map is assigned, it is a  factor multiply to the map value.

__Smoothness:__ this handle allows to set if a material is glossy or rough. If a mask map is assigned, it is a factor multiply to the map value.

__Mask map:__ it is a composited map. It has to be imported as a linear texture.

	Red channel: Metallic mask.

Green channel: Ambient occlusion.

Blue channel: Detail map mask.

Alpha channel: Smoothness map.

__Normal map space: __Normal can be set as tangent space or object space.

__Normal Map:__ assign the normal map. The handle can be used to refine normal strength.

__Bent normal map: __The bent normal is used to manage an occlusion with the indirect diffuse lighting (lightmap/lightprobe) - Cosine weighted Bent Normal Map (average unoccluded direction). Supported format: BC7, BC5, DXT5(nm). 

__Height Map:__ The red channel of the map assign is used as height map. It has to be imported as a linear texture.

* Parametrization: Min/Max or Amplitude.

  ![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/LayeredMaterialTemp/image_19.png)

Min: the lower value in the height map.

Max: the bigger value in the height map.

The value 0 match with the base mesh surface.

Offset: This value offset in world space the height map base.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/LayeredMaterialTemp/image_20.png)

Amplitude: It is the range between the min and the max value. The base is always at the middle of this value.

Base: It is the base position in the height texture space. (0= 0, 0.5= 128, 1= 255).

Offset: This value offset in world space the height map base.

__Base UV mapping:__ Define UV set between UV0, UV1, UV2, UV3, planar and triplanar. Pay attention about triplanar because it is really expensive. In case of planar and triplanar a world scale is used to define the world size of the material (Ex: 1= 1 meter, 0.5= 2 meters,...).

__Tiling:__ apply a tile factor to x/y.

__Offset:__ apply a UV position offset to x/y.

### 3.1.3 Detail Inputs:

The visibility of the detail texture is managed by the blue channel of the mask map.

__Detail map: __It is a blend map. Each channel is used to store informations about the detail map.  It has to be imported as a linear texture.

	Red channel: Albedo in grey.
	
	Green channel: Green channel of the normal map.
	
	Blue channel: Smoothness.
	
	Alpha channel: Red channel of the normal map.

__Detail UV mapping:__ Define UV set between UV0, UV1, UV2, UV3. If planar or triplanar UV are applied to the material, the detail texture uses too planar or triplanar UV.

Nb: lightmaps use UV1.

Lock to Base Tiling/Offset: If it is activated, the detail map tiling is multiply by the material tiling. In this case the tiling ratio between the material and the detail map is conserved.

__Tiling:__ apply a tile factor to x/y.

__Offset:__ apply an UV position offset to x/y.

__Detail AlbedoScale:__ handle to manage Albedo overlay of the detail map. Factor between 0 and 2.

__Detail NormalScale:__ handle to manage Normal add of the detail map. Factor between 0 and 2.

__Detail SmoothnessScale:__ handle to manage smoothness overlay of the detail map. Factor between 0 and 2.

## 3.2 Layer 1, 2, 3.

It is the same setting than the main layer except for Layering options

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/LayeredMaterialTemp/image_21.png)

__Use Opacity map as Density map:__ Base color alpha channel is used as opacity threshold instead of standard opacity.

The vertex color modulates the threshold. The effect depends if the vertex color mode is set to multiply or to add (See: [2-4 Inputs - Vertex color mode](#heading=h.vjd3knt382ta)).

0= full opacity, 1= full density.

Example with multiply mode (mask value is 1 by default):

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/LayeredMaterialTemp/image_22.jpg)

__BaseColor influence:__ Variance of the current layer is add to main layer.

__Normal influence:__ main layer Normal map is added.

__Heightmap influence:__ main layer Height map is added.

# 4 Emissive Inputs.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/LayeredMaterialTemp/image_23.png)

__Emissive Color:__ This texture is used as emissive. This texture is multiplied by the color. Default value is 1 if no texture is assigned and in this case only the color picker affects the emissive color.

__Base UV mapping:__ Define UV set between UV0, UV1, UV2, UV3, planar or triplanar.

__Tiling:__ apply a tile factor to x/y.

__Offset:__ apply an UV position offset to x/y.

__Emissive intensity:__ Manage the power of the emissive effect.

__Albedo Affect Emissive: __When activated the albedo is multiplied with the emissive color.

# 5 Advanced options.

__Enable GPU instancing:__ Enable it to create instance of similar objects with this material. GPU instancing and static batching can’t be used at the same time, GPU instancing has the priority.

__Enable Specular Occlusion from Bent normal:__ Enable it to use the Bent normal instead of the Ambient Occlusion map to manage the specular occlusion.

