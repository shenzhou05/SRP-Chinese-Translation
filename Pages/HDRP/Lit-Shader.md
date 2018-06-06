# The HD Render Pipeline Lit Shader

The lit shader is the default shader when using HDRenderPipeline (HDRP). This shader can be set with subsurface scattering, iridescence, vertex or pixel displacement and many other new parameters. This shader allows to users to produce more realistic assets with the use of HDRP. A version call LitTessellation is used to activate the tessellation.

## Creating a Lit Shader

In HDRP, when a new material is created it is by default a lit shader.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader1.png)

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader2.png)

## How to set a Lit Shader?

### Surface options

__Surface type:__

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader3.png)

Surface can be set as Opaque or Transparent. Transparent is an alpha blend and it is more costly.

__Alpha Cutoff:__

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader4.png)

This check box enable the alpha cutoff to use an alpha test. The handle set the value of the test. All the values under the handle value is totally transparent and the values equal or above the handle value is opaque.

__Double sided:__

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader5.png)

This option allows the double side. The faces are rendered on the two sides. The normal mode manages the normal behaviour on the backfaces. By default the mode is mirror.

__Material type:__

Material type introduces new behaviour for shaders to create realistic assets.

* Standard: Common use with basic parameters. The standard type uses a metallic workflow.

* Subsurface scattering (SSS): Mainly use to do a skin shader. This material type simulates the light transport inside a material and create softer micro shadows. 
Also a new parameter appears: Enable transmission. This parameter simulate the translucency of an object and it is managed by a thickness map.
SSS and transmission are setting by a diffusion profile explain later in this document.

* Anisotropy: The anisotropy determines the shape of the highlight. The surface vector is managed by a tangent map, an anisotropy map modulate the anisotropy intensity and a handle modulate and orient to horizontally or vertical the anisotropic effect. These parameters are more explain later in the documentation.

* Iridescence: Use to create an iridescent effect. The effect is modulate by an iridescence mask, iridescence thickness map and an handle iridescence thickness.

* Specular Color: Instead of standard type, the specular color type uses a specular workflow. In this way the specular can be colorize even for a not metallic matter.

* Translucent: This type is used to simulate only the transmission. It can be handy for vegetation and more light than a SSS type.This type use a profile like the SSS type to manage the transmission.

__Enable Decal:__

Allow the material to receive decals.

__Enable MotionVector For Vertex Animation:__

Use it to remove ghosting coming from vertex animation.

__Displacement mode:__

* None: no change.

* Vertex displacement: Use a height map to displace the vertices.

* Pixel displacement: Use a height map to displace the pixels. Use it only on plane surface. The surface can be only digged.

## Vertex animation / Enable wind


Prototype feature, don’t use it.

## Inputs

__Base color + opacity__: RGB channels are used as base color and alpha channel is used for opacity.

__Smoothness__ handle: This handle modulate (0 to 1) the smoothness value coming from the Mask map alpha channel.

__Mask map:__

* Red channel: Metallic mask. 0 = not metallic, 1 = metallic.

* Green channel: Ambient occlusion.

* Blue channel: Detail map mask.

* Alpha channel: Smoothness.

__Normal map space:__

By default the normal map space is in tangent space. The normal map space can be set to object space.

__Normal map:__

Use to assign the normal map. The handle modulate the normal intensity between 0 and 2.

__Bent normal map:__

The bent normal is used to have a better ambient occlusion. It works only with diffuse lighting like lightmap or light probe.

__Coat Mask:__

By default the value is 0. The mask is used to modulate the clear coat effect base on the handle value (0 to 1).

__Base UV mapping:__

UV can be set to UV0, UV1 (used by the lightmap), UV2, UV3, planar or triplanar.

Planar and triplanar use a world scale. This ratio depends about the size of the textures and the texel ratio wanted. By default it is 1, that means the material is applied on 1 meter. A value of 0.5 applies the material on 2 meters. 

__Tiling:__

Set the X/Y values to tile the material.

__Offset:__

Set on X/Y offset for the UV.

## Detail inputs

The detail map is a composited map used to add micro details into the material. The detail map visibility is managed by the blue channel of the Mask map.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader6.png)

__Detail map:__

* Red channel: Grey scale used as albedo.

* Green channel: Green channel of the detail normal map.

* Blue channel: Detail smoothness.

* Alpha channel: Red channel  of the detail normal map.

Channels are organised like this due the different compressions quality of each channels.

__Detail UV mapping:__

UV0, UV1, UV2 or UV3 can be set. If the material UV are set to planar or triplanar, the detail UV are also set to planar or triplanar.

__Lock to base Tiling/Offset:__

By default a detail texture is linked to the material aspect because it is done to add a micro detail in it. If for any reason the link have to be removed, just uncheck this checkbox.

__Tiling:__

Set the tiling of the detail texture inside a tile of the material. 
For example if the material is tiled by 2 on a plane and the detail texture is also tile by 2, the detail will appears tile by 4 on the plane.
In this condition the tile of the material can be changed without set another time the detail UV to keep the good appearance.

__Offset:__

Set on X/Y offset for the detail UV.

__Detail AlbedoScale:__

This handle modulate (0 to 2) the detail albedo (red channel) like an overlay effect. The default value is 1 and has no scale.

__Detail NormalScale:__

This handle modulate (0 to 2)  the intensity of the detail normal map. The default value is 1 and has no scale.

__Detail SmoothnessScale:__

This handle modulate (0 to 2)  the detail smoothness (blue channel) like an overlay effect. The default value is 1 and has no scale.

## Emissive inputs

__Emissive color:__

The emissive color can be managed by a map or a single color. If both are used they are multiplied.

__Emissive intensity:__

Set the power of the emissive effect. By default the value is 0 and doesn’t produce any emissive effect.

__Albedo Affect Emissive:__

By default it is on and allows the albedo to produce color for the emissive. In this case the albedo is multiplied by emissive color and color picker to produce the emissive final color.

For example the emissive color map can be used as an emissive mask, the albedo used to do the color and  the color picker to modulate it.

## Advanced options:

__Enable GPU instancing:__

If objects are not static batched and identical, all objects with this material become instanced.


For example, objects with an animation base on the object pivot can’t be static batched (unique pivot for all) but they can be instanced by GPU.

__Enable Specular Occlusion from Bent normal:__

This option used the bent normal assign in the bent normal slot to do a specular occlusion for the reflection probe.

## Specific setting from material type

### Subsurface scattering

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader7.png)

__Enable transmission: __

On/off the transmission effect. The transmission is managed by a profile and a thickness map. More the object is set thin more lighting cross it.

__Specific subsurface settings:__

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader8.png)

Diffusion profile:

Rollout menu to choose the profile. Profiles are set in the SSSSettings.asset file. Goto button select the the SSSSettings file.

Subsurface mask map:

This map uses the red channel to manage the visibility (0 = not visible, 1= totally visible) of the SSS effect. This map is modulated by the handle value (0 to 1, 1 is the default).

Thickness map:

This map uses the red channel to set the thickness inside the range set in the profile. 0 is the min range value and 1 is the max range value.

__The profile:__

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader9.png)

* Name: Name of the profile

* Scattering value: It is a HDR value to manage the color and the scatter of the SSS.

* Max radius: It is an information value and linked to the scattering value. It is the effective radius in millimeters. The blur is energy-preserving, so a wide result in a large area provides a small contribution of individual samples. A short distance increases the sharpness of the result.

* Index of Refraction: To set the real index of refraction. It is 1.4 for skin and between 1.3 and 1.5 for most other material.

* World scale: Set the size of the world unit in meters. Default it is 1 and shouldn’t be modified except if the world unit used is customized.

__Subsurface scattering only:__

Texturing mode: Specifies when the diffuse texture should be applied.

__Transmission only:__

Transmission mode: Regular or Thin object. Really thin object need a specific use.

Transmission tint: Set a HDR value to color the transmission.

Min/Max thickness (mm): Set the range of the thickness. This range is modulate by the thickness map (0 = min, 1 = max).

Thickness remap: This setting allows to remap the thickness without to change the min/max values. The range can be moved without losing the thickness values.

Profile preview: Shows the fraction of lights scattered from the source located in the center.The distance to the boundary of the image corresponds to the max radius. Display is not HDR, so the intensity of pixels around the center may be clipped.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader10.png)

Transmission preview: Shows the fraction of light passing through the object for thickness values from the remap. Can be viewed as a cross section of a slab of material illuminated by white light from the left.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader11.png)

### Anisotropy

Anisotropic materials don’t have an uniform specular shape.

Real anisotropy example:

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader12.png)

 Anisotropy is used to deform the specular shape on an axe.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader13.png)

__Tangent map: __

It is a vector map. Red and Green channel orient the specular shape.

__Anisotropy:__

This handle modulate the intensity of the anisotropic effect and modify the shape orientation, horizontally or vertically, coming from the tangent map.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader14.png)

__Anisotropy map:__

This map uses the red channel to modulate the anisotropic effect intensity.

### Iridescence

The iridescence (Thin-film interference) is a natural phenomenon in which lightwaves reflected by the upper and lower boundaries of a thin film interfere with one another, either enhancing or reducing the reflected[ ](https://en.wikipedia.org/wiki/Reflected_light)light. 

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader15.png)

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader16.png)

__Iridescence Mask:__

This map uses the red channel to manage the visibility of the iridescence effect. The handle can modulate the mask or the visibility if no mask is assigned.

__Iridescence Layer thickness map:__

If no map is assigned, by default the value is 1. The iridescence gradient color is linked to the thickness. When the thickness change the gradient color change too. The handle modulate the thickness also and it is multiplied when a map is assigned.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader17.png)

FYI: If the base color is white no iridescence can be visible. For a white base color no lighting enter the matter. All the lighting is reflected to produce a pure white color, so no iridescence can be produce.

### Specular color

When the specular color shader type is chosen, the specular color is defined by a dedicated map not anymore by the albedo value.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader18.png)

__Specular color:__

RGB map to set the specular color. When no map is assigned the default value is 1.

__Picker color:__

Uniform color used for the specular. It is multiply by the Specular color map.

## Translucent

The translucency is the transmission of a part of light across the matter.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader19.png)

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader20.png)

The translucency is manage by a profile and a thickness map like for the subsurface scattering.

## How to set a Lit Shader Tessellation?

From a lit shader, use the shader rollout menu to choose the LayeredLitTessellation shader.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader21.png)

In case of lit shader tessellation only standard, subsurface scattering and translucent types are available.

__Displacement mode:__

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader22.png)

None: No displacement is applied. The tessellation is used only to smooth the surface.

Tessellation displacement: A height map (red channel) is used in the inputs to displace the mesh vertices.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader23.png)

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader24.png)

* Lock with object scale: the height map appearance doesn’t change when the object is scaled.

* Lock with height map tiling rate: the height map appearance doesn’t change when the material is tiled.

__Tessellations options:__

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader25.png)

Tessellation mode:

* None: no smooth is aplied.

* Phong: the tessellation applied a smooth effect.

Tessellation factor:

Between 0 and 64 this factor modulate the tessellation quantity. Higher value mean a surface more tessellated. Above 15 is costly. For XBox one and Playstation4 the maximum is set to 15.

Start fade distance:

It is the distance (in Unity unit) to the camera where the tessellation start to fade out.

End fade distance:

It is the maximum distance (in Unity unit) to the camera where triangle are tessellated.

Triangle size:

Desired screen space size of triangle (in pixel). A smaller value mean smaller triangle.

__Height map parameterization:__

Two parametrizations are available.

Min/Max:

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader26.png)

In this mode the base of the height map is linked to the base of the mesh. It is used if the height map has uniform values on the map.

Min: Set the height value for the 0 value on the map.

Max: Set the height value for the 1 (255) value on the map.

Offset: Can up and down the height map without modify the min/max values.

Amplitude:

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/ScriptableRenderPipeline/HDRenderPipeline/Documentation/Images/LitShader27.png)

Amplitude mode is more used in case of height map with a dedicated center. In this case the height map uses often none uniform values. In case of non uniform values a range of the map is not used to store values, it is clamped in positive or negative.

Amplitude: The amplitude is the double value of the maximum value in negative or in positive.

Base: It is the reference of the base mesh into the height map. By default the base is at 0.5.

Offset: Can up and down the height map without modify the other values.

