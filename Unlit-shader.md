# Unlit #

The Unlit shader does not react to lights in the scene. Instead, a Sample [Global Illumination](https://docs.unity3d.com/Manual/GIIntro.html) option uses data that is baked into [Light Probes](https://docs.unity3d.com/Manual/LightProbes.html). 
Use this shader for stylised games or apps that do not require direct lighting. Because of the lack of light calculations, you can expect high performance from these games.

 
### Selecting this shader ###

To select and use this shader:
1. In your Project, create or find the Material you want to use the shader on.  Select the __Material__. A Material Inspector window opens. 
2. Click __Shader__, and select __Lightweight Render Pipeline__ > __Unlit__.

## UI overview ##

The Inspector window contains these elements: 
* __Render Properties__ 
* __Surface Properties__ 
* __Rendering Options__

You can read more about each section in the following overviews.

### Render Properties ###

The __Render Properties__ control how the material is rendered on a screen.

| Property | Description |
| ------------ | --- |
| __Surface Type__ | In this drop-down menu, choose between an __Opaque__ or __Transparent__ surface type. If you select __Transparent__, a second dropdown appears. See below.
| __Transparent__ surface type | Select __Alpha__ to use the alpha value to change how visible an object is. 1 is fully opaque, 0 is fully transparent. Select  __Premultiply__ to the same as __Alpha__, but only to diffuse textures. This means that only the reflected light is visible, not objects in the reflection. For example, like a glass texture. Select _Additive__ to add an extra layer on top of another surface. This is good for holograms. Select __Multiply__ to multiply the colors behind the surface, like colored glass. |
| __Two Sided__ | Enable this to render on both sides of your geometry. When disabled, Unity [culls](https://docs.unity3d.com/Manual/SL-CullAndDepth.html) the backface of your geometry and only renders the frontface. For example, Two Sided rendering is good for small, flat objects, like leaves, where you might want both sides visible. By default, this setting is disabled, so that backfaces are culled. |
| __Alpha Clip__ | Enable this to make your Material act like a [Cutout](https://docs.unity3d.com/Manual/StandardShaderMaterialParameterRenderingMode.html) shader. With this, you can create a transparent effect with hard edges between the opaque and transparent areas. For example, to create straws of grass. This effect happens, because the Alpha values below a given threshold are not rendered. If you enable this feature, a __Clip Threshold__ slider appears. Here, select an offset where you want to clip the alpha values.|

### Surface Properties ###
The __Surface Properties__ describe the surface itself. For example, you can use these properties to make your surface look wet, dry, rough, or smooth. 

| Property | Description |
| ------------ | --- |
__MainTex__ | This is the color of the surface, also known as the diffuse map. To assign a texture to the __MainTex__ setting, click the object picker next to it. This opens the Asset Browser, where you can select among the textures on your project. Alternatively, you can use the [color picker](https://docs.unity3d.com/Manual/EditingValueProperties.html). The color next to the setting shows the tint on top of your assigned texture. To assign another tint, you can click this color swatch. If you have selected __Transparent__ or __Alpha Clip__ under __Render Properties__, your __Material__ uses the texture’s Alpha channel or color.
__Sample GI__ | With this enabled, you can create a surface that uses [Light Probe](https://docs.unity3d.com/Manual/LightProbes.html) data to add ambient lighting. When enabled, the setting __Normal map__ appears. Here, you can assign a tangent-space [normal map](https://docs.unity3d.com/Manual/StandardShaderMaterialParameterNormalMap.html), similar to the one in the Standard Shader in the built-in render pipeline. To read more about tangent-spaced normal maps, [see this article on Polycount](http://wiki.polycount.com/wiki/Normal_Map_Technical_Details#Tangent-Space_vs._Object-Space). If you do not enable __Sample GI__, the render pipeline considers ambient as white and skips sampling the Light Probe data.
__Tiling__ | A 2D multiplier value that scales the texture to the fit across a mesh according to the U and V axes. This is good for surfaces like floors and walls. The default value is 1, which means no scaling. Set a higher value to make the texture repeat across your mesh. Set a lower value to stretch the texture. There are no upper and lower limits, so try different values until you reach your desired effect.
__Offset__ | The 2D offset that positions the texture on the mesh.  To adjust the map position on your mesh, move the texture across the U or V axes.

### Rendering Options

The __Rendering Options__ settings affect behind-the-scenes rendering. They do not have a visible effect on your surface, but on underlying calculations.

Property | Description
---|---
__GPU Instancing__ | Allow meshes with the same geometry and material/shader to be rendered in one batch, if they can. This makes rendering faster.  Meshes cannot be rendered in one batch if they have different materials or if the hardware does not support GPU instancing. 
__Double Sided Global Illumination__ | Make the surface act double-sided during lightmapping. When enabled, backfaces bounce light like frontfaces, but they are still not rendered. 


