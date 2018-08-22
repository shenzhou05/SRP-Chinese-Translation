The Physically Based shader lets you render real-world surfaces like stone, wood, glass, plastic, and metals in photo-realistic quality. Your light levels and reflections look right and react properly across various lighting conditions, for example bright sunlight, or a dark cave.


## Using the Physically Based shader in the Editor ##
You can either create a new material with the shader or select the shader from the Material inspector.

To create a new material with the shader:
1. In your Project window, click __Create__ > __Material__. Select the __Physically Based__ shader.

To select the shader in the Material inspector:
1. In your Project, select the __Material__ Inspector. 
2. Click __Shader__, and select __Lightweight Render Pipeline__ > __Physically Based__.

## UI overview ##
The Inspector window contains these elements: 

* __Render Properties__
* __Surface Properties__
* __Rendering Options__

![Standard (Physically Based) inspector](https://raw.githubusercontent.com/Unity-Technologies/SRPDocContent/master/LWRP/Images/Inspectors/Shaders/StdPhysicallyBased.png)



### Render Properties ##

The __Render Properties__ control how the material is rendered on a screen. 


| Property | Description |
| ------------ | --- |
| __Workflow Mode__ | In this drop-down menu, choose a workflow that fits your textures, either  __Metallic__ and __Specular__. Once you have made your choice, the main texture options now follow your chosen workflow. To see more about metallic or specular workflows, see [this Manual page for the Standard built-in shader in Unity](https://docs.unity3d.com/Manual/StandardShaderMetallicVsSpecular.html). |
| __Surface Type__ | In this drop-down menu, choose between an __Opaque__ or __Transparent__ surface type. If you select __Transparent__, a second dropdown appears. See below.
| __Transparent__ surface type | Select __Alpha__ to use the alpha value to change how visible an object is. 1 is fully opaque, 0 is fully transparent. Select  __Premultiply__ to the same as __Alpha__, but only to diffuse textures. This means that only the reflected light is visible, not objects in the reflection. For example, like a glass texture. Select __Additive__ to add an extra layer on top of another surface. This is good for holograms.Select __Multiply__ to multiply the colors behind the surface, like colored glass. |
| __Two Sided__ | Enable this to render on both sides of your geometry. When disabled, Unity [culls](https://docs.unity3d.com/Manual/SL-CullAndDepth.html) the backface of your geometry and only renders the frontface. For example, Two Sided rendering is good for small, flat objects, like leaves, where you might want both sides visible. By default, this setting is disabled, so that backfaces are culled. |
| __Alpha Clip__ | Enable this to make your Material act like a [Cutout](https://docs.unity3d.com/Manual/StandardShaderMaterialParameterRenderingMode.html) shader. With this, you can create a transparent effect with hard edges between the opaque and transparent areas. For example, to create straws of grass. This effect happens, because the Alpha values below a given threshold are not rendered. If you enable this feature, a __Clip Threshold__ slider appears. Here, select an offset where you want to clip the alpha values.|



### Surface Properties ##

The __Surface Properties__ describe the surface itself. For example, you can use these properties to make your surface look wet, dry, rough, or smooth. 

**Note:** If you are used to the [Standard Shader](https://docs.unity3d.com/Manual/shader-StandardShader.html) in the built-in Unity render pipeline, these options are similar to the Main Maps settings in the [Material Editor](https://docs.unity3d.com/Manual/StandardShaderContextAndContent.html).



| Property | Description |
--- | ---
__Albedo__ | The [albedo](https://docs.unity3d.com/Manual/StandardShaderMaterialParameterAlbedoColor.html) specifies the color of the surface. It is also known as the diffuse map. To assign a texture to the __Albedo__ setting, click the object picker next to it. This opens the Asset Browser, where you can select among the textures currently in your project. Alternatively, you can use the [color picker](https://docs.unity3d.com/Manual/EditingValueProperties.html). The color next to the setting shows the tint on top of your assigned texture. To assign another tint, you can click this color swatch. If you have selected __Transparent__ or __Alpha Clip__ under __Render Properties__, your __Material__ uses the texture’s Alpha channel or color.
__Metallic / Specular__ | Shows a map input for your chosen __Workflow Mode__ in the __Render Properties__.  For a [Metallic](https://docs.unity3d.com/Manual/StandardShaderMaterialParameterMetallic.html) map, a slider appears, and for a [Specular map](https://docs.unity3d.com/Manual/StandardShaderMaterialParameterSpecular.html), a color input appears. For both map types, __Smoothness__ controls the spread of highlights and/or reflections on the surface. Under __Source__, you can control where to sample smoothness map from. By default, Source uses the Alpha channel for either map. You can also set it to the Albedo Alpha channel.
__Normal Map__ | Assign a tangent-space [normal map](https://docs.unity3d.com/Manual/StandardShaderMaterialParameterNormalMap.html), similar to the one in the Standard Shader in the built-in render pipeline. To read more about tangent-spaced normal maps, [see this article on Polycount](http://wiki.polycount.com/wiki/Normal_Map_Technical_Details#Tangent-Space_vs._Object-Space). The float value next to the setting is a multiplier for the effect of the  __Normal Map__.
__Occlusion__ | Select an occlusion map to simulate shadowing of ambient light. 
__Emission__ | Make the surface emit light. When enabled, the  __Texture map__ and __HDR color__ settings appear. If you do not enable this, emission will be considered as black, and Unity skips calculating emission. 
__Tiling__ | A 2D multiplier value that scales the texture to the fit across a mesh according to the U and V axes. This is good for surfaces like floors and walls. The default value is 1, which means no scaling. Set a higher value to make the texture repeat across your mesh. Set a lower value to stretch the texture. There are no upper and lower limits, so try different values until you reach your desired effect.
__Offset__ | The 2D offset that positions the texture on the mesh.  To adjust the map position on your mesh, move the texture across the U or V axes.
__Specular Highlights__ | Enable this to allow your material to have specular highlights from direct lighting, for example [Directional, Point, and Spot lights](https://docs.unity3d.com/Manual/Lighting.html). This means that your material reflects the shine from these light sources. Disable this to leave out these highlight calculations, so your shader renders faster. By default, this feature is enabled.
__Reflections__ | Sample reflections using the nearest [Reflection Probe](https://docs.unity3d.com/Manual/class-ReflectionProbe.html), or, if you have set one in the [Lighting](https://docs.unity3d.com/Manual/GlobalIllumination.html) window, the [Lighting Probe](https://docs.unity3d.com/Manual/LightProbes.html). Disabling sampling saves on calculations, but also means that your surface has no reflections.

### Rendering Options

The __Rendering Options__ settings affect behind-the-scenes rendering. They do not have a visible effect on your surface, but on underlying calculations.

Property | Description
---|---
__GPU Instancing__ | Allow meshes with the same geometry and material/shader to be rendered in one batch, if they can. This makes rendering faster.  Meshes cannot be rendered in one batch if they have different materials or if the hardware does not support GPU instancing. 
__Double Sided Global Illumination__ | Make the surface act double-sided during lightmapping. When enabled, backfaces bounce light like frontfaces, but they are still not rendered. 

## The technology in this shader ##
This shader follows standard rules for Physically Based Rendering (PBR).To read more about Physically Based Rendering, see [this walkthrough by Joe Wilson on Mamoset](https://marmoset.co/posts/physically-based-rendering-and-you-can-too/).  The shader is energy conserving, which means that the surface never reflects more light than the total incoming light.

For specular reflections, the shader uses a [Bidirectional Reflectance Distribution Function (BRDF)](https://en.wikipedia.org/wiki/Bidirectional_reflectance_distribution_function) that uses [GGX](https://blogs.unity3d.com/2016/01/25/ggx-in-unity-5-3/) to control the shape of the specular highlight. 
For diffuse reflections, it uses a [lambertian reflectance](https://en.wikipedia.org/wiki/Lambertian_reflectance) model.

This shader uses [channel packing](http://wiki.polycount.com/wiki/ChannelPacking), so you can use a single RGBA texture for the metallic, smoothness and occlusion properties. When you use texture packing, you only have to load one texture into memory instead of three separate ones. When you write your texture maps in a program like Substance or Photoshop, you can pack the maps like this:

| Channel | Property |
| --- | ---|
| **Red** | Metallic |
| **Green** | Occlusion |
| **Blue** | None. |
| **Alpha** | Smoothness |







