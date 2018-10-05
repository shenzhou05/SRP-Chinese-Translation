# The Terrain Lit Shader

The terrain lit shader is the specific shader used on terrain. This shader is a simpler version of HDRP lit shader with diffuse, normal and mask map. 
A Terrain can use 1 to 8 layers with one material assigned to a layer.

## Creating a Terrain layer

- Select a terrain,
- Activate paint terrain:

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/936b0c1bb82c6854ff10dfae111241fcc7112f71/com.unity.render-pipelines.high-definition/Documentation~/Images/TM-Screen01.jpg?raw=true)
- Click on Edit Terrain Layers button and choose “Create Layer” or use “Add Layer” to add an existing material already done with a previous terrain:

![](https://raw.githubusercontent.com/Unity-Technologies/ScriptableRenderPipeline/dbf9a4d0dd22513eb7ea4fd10558d82d2c548a7a/com.unity.render-pipelines.high-definition/Documentation~/Images/TM-Screen02.jpg)

- Select a texture 2D, it will be set to the diffuse slot,
- A terrain layer vignette appear in the terrain layer list:

![](https://raw.githubusercontent.com/Unity-Technologies/ScriptableRenderPipeline/dbf9a4d0dd22513eb7ea4fd10558d82d2c548a7a/com.unity.render-pipelines.high-definition/Documentation~/Images/TM-Screen03.jpg)

Use the “open” button on top of the diffuse vignette to select the material in the project to be able to rename or to move it in the project.

## How to set a Terrain Lit Shader?

### Diffuse:

The diffuse color is defined by a 2D texture multiplied by a color tint.
If the 2D texture as an alpha channel, it can be set as opacity or density. The default setting is the opacity mode. The check box is used to switch to density mode.

In case of opacity the alpha is used as alpha blend.
In case of density, the alpha channel is used as a threshold. This threshold is managed by the brush opacity.

### Normal:

The normal map setting is composed by a normal map texture and a scale value. This scale value is to up and down the normal map intensity effect.
The scale value is available only when a normal map texture is assigned.

### Mask map:
This is a composed texture to manage metalness, ambient occlusion and smoothness. This format it is the same than the HDRP lit shader.
Red channel: Metalness,
Green channel: Ambient occlusion,
Blue channel: Not used,
Alpha channel: Smoothness.

Nb: Alpha channel is used for the smoothness instead of blue channel to reduce compression effect to have the best visual result. A good smoothness has an important effect to the final rendering.

### Mask map channel setting:
If no texture is assigned into the Mask map texture slot, the metalness, the ambient occlusion and the smoothness values are managed by handles. The values are between 0 and 1.

![](https://raw.githubusercontent.com/Unity-Technologies/ScriptableRenderPipeline/dbf9a4d0dd22513eb7ea4fd10558d82d2c548a7a/com.unity.render-pipelines.high-definition/Documentation~/Images/TM-Screen04.jpg)

If a texture is assigned into the Mask map texture slot, the values are managed by the texture. The min/max values can be remap by handles.

![](https://raw.githubusercontent.com/Unity-Technologies/ScriptableRenderPipeline/dbf9a4d0dd22513eb7ea4fd10558d82d2c548a7a/com.unity.render-pipelines.high-definition/Documentation~/Images/TM-Screen05.jpg)

## Tiling setting:

Size is defined in meter. A value of 1 means that the texture is repeat every meter.
Offset is in meter too. The offset allows to move the UV origin.

Size and offset can be set on X and Y world axis.
