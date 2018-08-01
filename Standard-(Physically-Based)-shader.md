The Standard (Physically based) shader lets you render “real-world” surfaces. You can render stone, wood, glass, plastic, or metals in photo-realistic quality. The shader works across different lighting conditions.

This shader follows standard rules for Physically Based Rendering (PBR). The shader uses a simplified GGX shading model. 

## Using this shader ##
You can find this shader in two different ways. Either create a new material with the shader, or select the shader from the Material inspector.

To create a new material with the shader:
In your Project window, click Create > Material. Select the Standard (Physically Based) shader.

To select the shader in the Material inspector:
In your Project, select the Material Inspector. Click Shader, and select Lightweight Render Pipeline > Standard (Physically Based).

## UI overview ##
The Inspector window contains these elements: 
Render Properties
Surface Properties
Rendering Options.

![Standard (Physically Based) inspector](https://raw.githubusercontent.com/Unity-Technologies/SRPDocContent/master/LWRP/Images/Inspectors/Shaders/StdPhysicallyBased.png)

### Render Properties ##

The __Render Properties__ control how the material is rendered on a screen. 

Overview of Render Properties:

| Property | Description |
| ------------ | --- |
| __Workflow Mode__ | In this dropdown, choose a workflow that fits your textures. You can choose between __Metallic__ and __Specular__. |
| __Surface Type__ | In this dropdown, choose between an Opaque or Transparent surface type. If you select Transparent, a second dropdown appears. Here, select either __Alpha__, __Premultiply__, __Additive__, or __Multiply__. |
| __Two Sided__ | Enable this to turn off Culling. When culling is turned off, both sides of your geometry will be rendered.|
| __Alpha Clip__ | Enable this make your Material act like a Cutout shader. This means that Alpha values below 0 are not rendered. If you enable this, a __Clip Threshold__ slider appears. Here, select an offset where the clip happens.|



### Surface Properties ##

The __Surface Properties__ describe the surface itself. These are similar to the Maps section in the built-in Standard shader.

Overview of Surface Properties:

Property | Description
--- | ---
__Albedo__ | This is the color of the surface, also known as the diffuse map. You can either assign a texture to it, or use the color picker. The color next to the setting shows the multiplicative tint on top of your assigned texture. If you have selected __Transparent__ or __Alpha Clip__ under __Render Properties__, these use the Alpha channel of your texture or color.
__Metallic / Specular__ | This setting shows a map input for your chosen __Workflow Mode__ under __Render Properties__.  For a Metallic map, a slider appears, and for a Specular map, a color input appears. __Smoothness__ controls the spread of highlights and/or reflections on the surface. Under __Source__, you can control where to sample smoothness map from. By default, Source uses the Alpha channel for either map. You can also set it to the Albedo Alpha channel.
__Normal Map__ | Here, you can assign a tangent space normal map. The float value next to the setting is a multiplier for the __Normal Maps__ effect.
__Occlusion__ | Indicates the occlusion map that simulates shadowing of ambient light. If you’re using the Metallic workflow, you can also use the Metallic map, if the Occlusion is packed into the G channel.
__Emission__ | Enable this to be able to create a surface that emits light. When enabled, the settings  __Texture map__ and __HDR color__ appear. If you do not enable this, emission will be considered as black, and Unity skips calculating emission. 
__Tiling__ | The 2D scale value for your texture. This is a multiplier value. Set a high value to make the texture repeat across your mesh. Set a low value to stretch the texture. 1 is the default value, which denotes no scaling. 
__Offset__ | The 2D offset of your texture.  To adjust the map position on your mesh, move the texture across the U or V axes.
__Specular Highlights__ | Enable this to allow shaders to have highlights from direct lights, for example Directional, Point, and Spot lights. Disable this to leave out these light calculations.
__Reflections__ | Enable this to use sampling of reflections. Sampling uses the nearest Reflection Probe, or, if you have set one, the Lighting Probe from Lighting Settings. Disabling sampling saves on calculations, but also means that you have no reflections.

### Rendering Options

The __Rendering Options__ settings affect “behind-the-scenes” rendering. They do not have a visible affect on your surface, but on underlying calculations.

Property | Description
---|---
__GPU Instancing__ | Enable this to allow meshes with the same geometry and material/shader to be rendered in one batch. To be rendered in one batch, if they can.
__Double Sided Global Illumination__ | Enable this to make the surface act double-sided during lightmapping. 



