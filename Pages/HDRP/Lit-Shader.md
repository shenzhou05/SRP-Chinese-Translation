# HDRP Lit Shader

The Lit Shader includes options for subsurface scattering, iridescence, vertex or pixel displacement and many other parameters. This Shader lets you easily create realistic materials with minimal configuration. For more information about Materials, Shaders and Textures, see the [Unity User Manual](https://docs.unity3d.com/Manual/Shaders.html). 

By default, new materials created in HDRP are assigned the Lit Shader, with all properties empty as shown in the image below: 

![1538142195818](C:\Users\robsh\AppData\Roaming\Typora\typora-user-images\1538142195818.png)

## Creating a Lit Shader

To create a new Lit Shader Material, navigate to your Project's Asset window, right-click the Asset Window and select **Create > Material.** The newly created Material will then be added to your Project's Asset folder. 

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader1.png)

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader2.png)

## Lit Shader Parameters

##Surface options

Surface options control the overall look of your Material's surface and how Unity renders the Material on screen.  

* **Surface type**: The Surface Type options control the transparency of your Shader. 
     * **Opaque**: Opaque simulates a completely solid Material, with no light penetration. 
     * **Transparent**: Transparent simulates a translucent material that light can penetrate, such as clear plastic or glass. The Transparent surface option uses alpha blending and is more costly to render than an opaque Shader. 

* __Alpha Cutoff:__

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader4.png)

Enable this to make your Material act like a [Cutout](https://docs.unity3d.com/Manual/StandardShaderMaterialParameterRenderingMode.html) Shader. With this, you can create a transparent effect with hard edges between the opaque and transparent areas. Unity achieves this effect by not rendering Alpha values below the value specified in Alpha Cutoff field.

__Double sided:__

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader5.png)

Enable this to render on both sides of your geometry. When disabled, Unity [culls](https://docs.unity3d.com/Manual/SL-CullAndDepth.html) the backface of your geometry and only renders the frontface. For example, **Double Sided** rendering is good for small, flat objects, like leaves, where you might want both sides visible. By default, this setting is disabled, so that Unity culls backfaces.

__Material type:__

The Material Type dropdown displays different settings depending on the Material Type selected. Each Material Type has a different workflow and and you should use the Material Type that is most suitable for the Shader you are creating (SSS for skin and foliage, )

* **Standard**: Uses the basic parameters and is the default Material type. Standard uses a basic metallic shader workflow

* **Subsurface scattering (SSS)**: SSS simulates the way light interacts with and penetrates translucent objects, such as skin or plants. When light penetrates the surface of a SSS Material it is scattered and blurred by interacting with the material before exiting the surface at a different point. 

  * **Enable Transmission** (SSS only) : This parameter simulates the translucency of an object and it is managed by a thickness map. 
    SSS and transmission settings are configured using a [Diffusion Profile](#SSS), which is explained below. .

  See documentation on [Subsurface Scattering]() and [Transmission]() for more information. 

* **Anisotropy**: The highlights of Anisotropic surfaces change in appearance as the Material is rotated relative to the camera. Use the Anisotropy Material Type to create Materials that require anisotropic highlights, for example: brushed metal or velvet. 

  See the below section on [Anisotropy](link) for more information. 

* **Iridescence**: Iridescent surfaces appear to gradually change colour as the angle of view or angle of illumination changes. Use the Iridescence Material Type to create materials like soap bubbles, iridescent metal or insect wings. 

   See the below section on [Iridescense](link) for more information. 

* **Specular Color**: Use The Specular Colour Material Type to create Materials with a coloured specular highlight. This Material Type is similar to the [built-in Specular Shader](https://docs.unity3d.com/Manual/StandardShaderMaterialParameterSpecular.html), but you can disable energy conservation by unticking the **Energy Conserving Specular** checkbox.

* **Translucent**: Use The Translucent Material Type to simulate a translucent material using a thickness map. In contrast to SSS Materials, Translucent Materials only transmit light through the Material, without blurring the light.

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

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader6.png)

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

<a name="SSS"></a>

### Subsurface scattering

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader7.png)

__Enable transmission: __

On/off the transmission effect. The transmission is managed by a profile and a thickness map. More the object is set thin more lighting cross it.

__Specific subsurface settings:__

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader8.png)

Diffusion profile:

Rollout menu to choose the profile. Profiles are set in the SSSSettings.asset file. Goto button select the the SSSSettings file.

Subsurface mask map:

This map uses the red channel to manage the visibility (0 = not visible, 1= totally visible) of the SSS effect. This map is modulated by the handle value (0 to 1, 1 is the default).

Thickness map:

This map uses the red channel to set the thickness inside the range set in the profile. 0 is the min range value and 1 is the max range value.

__The profile:__

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader9.png)

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

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader10.png)

Transmission preview: Shows the fraction of light passing through the object for thickness values from the remap. Can be viewed as a cross section of a slab of material illuminated by white light from the left.

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader11.png)

### Anisotropy

Anisotropic materials don’t have an uniform specular shape.

Real anisotropy example:

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader12.png)

 Anisotropy is used to deform the specular shape on an axe.

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader13.png)

__Tangent map: __

It is a vector map. Red and Green channel orient the specular shape.

__Anisotropy:__

This handle modulate the intensity of the anisotropic effect and modify the shape orientation, horizontally or vertically, coming from the tangent map.

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader14.png)

__Anisotropy map:__

This map uses the red channel to modulate the anisotropic effect intensity.

### Iridescence

The iridescence (Thin-film interference) is a natural phenomenon in which lightwaves reflected by the upper and lower boundaries of a thin film interfere with one another, either enhancing or reducing the reflected[ ](https://en.wikipedia.org/wiki/Reflected_light)light. 

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader15.png)

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader16.png)

__Iridescence Mask:__

This map uses the red channel to manage the visibility of the iridescence effect. The handle can modulate the mask or the visibility if no mask is assigned.

__Iridescence Layer thickness map:__

If no map is assigned, by default the value is 1. The iridescence gradient color is linked to the thickness. When the thickness change the gradient color change too. The handle modulate the thickness also and it is multiplied when a map is assigned.

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader17.png)

FYI: If the base color is white no iridescence can be visible. For a white base color no lighting enter the matter. All the lighting is reflected to produce a pure white color, so no iridescence can be produce.

### Specular color

When the specular color shader type is chosen, the specular color is defined by a dedicated map not anymore by the albedo value.

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader18.png)

__Specular color:__

RGB map to set the specular color. When no map is assigned the default value is 1.

__Picker color:__

Uniform color used for the specular. It is multiply by the Specular color map.

## Translucent

The translucency is the transmission of a part of light across the matter.

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader19.png)

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader20.png)

The translucency is manage by a profile and a thickness map like for the subsurface scattering.

## How to set a Lit Shader Tessellation?

From a lit shader, use the shader rollout menu to choose the LayeredLitTessellation shader.

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader21.png)

In case of lit shader tessellation only standard, subsurface scattering and translucent types are available.

__Displacement mode:__

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader22.png)

None: No displacement is applied. The tessellation is used only to smooth the surface.

Tessellation displacement: A height map (red channel) is used in the inputs to displace the mesh vertices.

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader23.png)

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader24.png)

* Lock with object scale: the height map appearance doesn’t change when the object is scaled.

* Lock with height map tiling rate: the height map appearance doesn’t change when the material is tiled.

__Tessellations options:__

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader25.png)

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

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader26.png)

In this mode the base of the height map is linked to the base of the mesh. It is used if the height map has uniform values on the map.

Min: Set the height value for the 0 value on the map.

Max: Set the height value for the 1 (255) value on the map.

Offset: Can up and down the height map without modify the min/max values.

Amplitude:

![](C:\Users\robsh\Documents\GitHub\ScriptableRenderPipeline.wiki\Images\HDRP\LitShader27.png)

Amplitude mode is more used in case of height map with a dedicated center. In this case the height map uses often none uniform values. In case of non uniform values a range of the map is not used to store values, it is clamped in positive or negative.

Amplitude: The amplitude is the double value of the maximum value in negative or in positive.

Base: It is the reference of the base mesh into the height map. By default the base is at 0.5.

Offset: Can up and down the height map without modify the other values.

