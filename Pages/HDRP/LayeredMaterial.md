 

# Layered material 

 

The layered material is used to stack 2 to 4 materials on the same object. This material can be helpful to create diversity or to integrate objects between them.

The cost of this material is more heavy than a standard material, so use it when it is needed.

The layered material uses the HDRenderPipeline

# 1 Create a layered material.

First step is to create a material.

![img](https://lh4.googleusercontent.com/Sd7PmkrIxNlvhSZgO3Xh0rPScrSVFmVZzgCduShh-yWF3773hNouO657VZpRf1z-jRRJqREI0RZ0CZM4uXfJxKzO-m1BfSynskD4UHqBOkEL53QwH9lW_OJ2Nw-ofWjm9SrdMQQo)

 

Modify shader to LayeredLit or LayeredLitTessellation. It depending if the tessellation is needed.

![img](https://lh3.googleusercontent.com/hKssRLFGBqbMYFtOxD-9Ci16azDby_pRVb5w9z0UJeXf23M7f49vnxZW1vNdcPuALg_kR3bZFKjcTI7_myw3TGmmVs8uHOcJaiRUgm0JFcJ1OwYfxpyDLet06nn3GSKfVFwi2q_q)

# 2 Layered material setting.![img](https://lh6.googleusercontent.com/bbsKu-LzZZa7dD2SbMOQOAQFkAcb-kBI2m-JR3QlK8YVDkHIrxEasibvvpc0YWzSx1tQocHhG2NBfPJPdOQ1dZFC5RyXkR3Ib5svNFOnKaAxv_VH8Gj2b9dvmvuCtf2UoCip-aZN)

 

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

 

![img](https://lh4.googleusercontent.com/o70aumBg11lE9osurCY-uM0eKOPyVMRJ-u9PmxBtu19-3PbFuKWefAlT_xjT8nMVQHQQomofEedoqJ_FGJLqPkosC_kyV7CuM6SbxaJz-HrjfhH9FeI06GBdrBKeKK41SX9dxL8z)

 

Surface type: Opaque or transparent.

Transparent options:

![img](https://lh6.googleusercontent.com/N5ChehckcXyiiq28kgnUmwnkqYD-hharUjs3qOkhq43eTZtzC_RVlAOhd2X_f4bf9lgSRDwadBAoG-or7UxQuwECzjptapfuRn53sFRqEF9SpGiMpUajtYqj-NFybQnKzmRwczaM)

- Blend mode: Alpha (default), Additive, PremultipliedAlpha.
  (<https://docs.unity3d.com/Manual/SL-Blend.html>)

- Blend preserve specular lighting: Blend mode will only affect direct lighting, allowing correct specular lighting (reflection) on transparent object.
- Enable Fog: Enable fog on transparent object.
- Pre Refraction Pass: Render objects before the refraction pass.
- Transparent Sort Priority: Allow to define priority (from -100 to +100) to solve sorting issue with transparent.

 

 

Alpha Cutoff: To enable alpha test (0 transparent, 1 opaque). Alpha cutoff has an handle to define the threshold between transparent and opaque.

 

Double side: Enable double side. Normal can be set to mirror (default) or flip.

 

Material type: Standard or Subsurface Scattering and Transmission

 

Subsurface Scattering and Transmission type:

- Both
- SSS only
- Transmission only

 

Enable Decal: Allow to specify if the material can receive decal or not.

 

Enable MotionVector For Vertex Animation: This will enable an object motion vector pass for this material. Useful if wind animation is enabled or if displacement map is animated.

Displacement mode:

 

Tesselation activated:

 

Displacement mode: none or tessellation displacement.

 

- None: tessellation can be used only to smooth the geometry without any heightmap.

 

![img](https://lh4.googleusercontent.com/d1QEYFPNAv5RUeqYjw5v-ysRhUPpQvMEe9PZ3D6SpRaSjW-DslzflRLugfuVVwqE-IBp0NomU1bWmzTrIQYclkJXbCZCXxmOP41Ym_N1tM5ScyVuPSjupRdBwV0h9AAOVXMa6ZT1)

 

 

- Tessellation displacement: height map is used to manage the displacement with the tessellation.

 

Tessellation displacement option:

- Lock with object scale: when activate the object scale keeps the height map appearance.
- Lock with height map tilling rate: the material tiling keeps the height map appearance.

 



Tessellation displacement example:

![img](https://lh4.googleusercontent.com/i8yHOPWJ3XGuQ8CueF5WYzq7GyzT_uh3L-7uZ92XvpoikxyTrLKYSe4IPDIm9wHUtwDC_Vcii3g_O_Y1Wcb_7khBbOQqYh7SHD6GLs6UG1yjFo_Fi6vudtA6BBFwgamkiJMo7f3o)

 



Tessellation not activated:

 

Displacement mode: none, vertex displacement or pixel displacement.

 

- None: do nothing.

 

- Vertex displacement: use height map to move vertices.

![img](https://lh3.googleusercontent.com/d-roELaUllSLMNijdELi3Ge_LuEVSE23wSpH1iIWZxlEtokcBS_FgUqkGQJUalbWhBqkjKSWPaj2ImaEtF_N97ttospYkEvYB07BZogGYftltZBkJwXGx_ftchxNjJNwGmaxYFbl)

Vertex displacement option:

- Lock with object scale: when activate the object scale keeps the height map appearance.
- Lock with height map tilling rate: the material tiling keeps the height map appearance.

 

Vertex displacement example:

![img](https://lh6.googleusercontent.com/cKsdT27FvuztEld0kPYd79L8Qa5Alv7RGa3snUJEajd18GY5QA5A8HAAS7w0Az1Z4K2bInxoIDbN4IpGD3pSGPiznKCnmxOEx98LmbJ8oOcaX5qnWtdBcFXA7Czw6jJxGiZJwmuz)

 

 

- Pixel Displacement: Enable the parallax occlusion mapping. Parallax occlusion mapping can only dig base on the height map. Use it only on flat surfaces.

![img](https://lh3.googleusercontent.com/0oKboQdWayNjs2mq0psU2nwNrM-dr2O0MsdVMQUP_nnFMlji3Qrw2S9Br2xKuToGn8aVHqltC4IZiwNTg4tSLZ6bgIDbZtX2uTFQ-rpYZbc-04VugFD0vjkJcY5E4Hn_MLZKHf-1)

 

Pixel displacement option:

- Lock with object scale: when activate the object scale keep the height map appearance.
- Lock with height map tilling rate: the material tiling keep the height map appearance.
- Minimum steps: Minimum steps (texture sample) to use with per pixel displacement mapping.
- Maximum steps: Maximum steps (texture sample) to use with per pixel displacement mapping.
- Fading mip level start: Starting heightmap mipmap lod number where the parallax occlusion mapping effect start to disappear.
- Primitive length: let it at 1.
- Primitive width:  let it at 1.
- Enable Depth Offset: Enable depthOffset on this shader (use with heightmap).

 

 



Per pixel displacement example:

![Pom.jpg](https://lh6.googleusercontent.com/DAZhiNKZS_BqqYIlyk-Wc-nml2C5UjYy4itE0iKoD6k7ozovoKfuo54Ey1WHg9LvXmLiSu2Q-uLeCHSUSJFCwvD6ga3Q7ToKt1YApScwVGMb4FI-MBwSfRl33jRDfiHC8o2tn_Yw)

 

 

 

## 

## 2.2 Tessellation options.

![img](https://lh5.googleusercontent.com/9WUFyzYTJiYG7NcUsOrIyZvfWso9vQuqi2Wp5jHjpSmmRfGt4Y7ShKQojBXb0MaFtLTd1q4KA-jxczIDghC4QZHygNniyY0jDCu2NCrvgu8UJR1DJJqYuSZ8i1gibR2WxE3MYYt8)

 

Tessellation Mode: None or Phong.

 

- None: Linear tessellation between two vertices,
- Phong: Smooth tessellation between two vertices.

 

![img](https://lh5.googleusercontent.com/BwMrQkojhC-fgec6Kw90F29Zn2QZ7GTLrKrglMay45tdb__G3rW8jcgW4mYla3jYVbsjC4RvgIhYOKDa7tCoL4wMKEzmSVcZZxaOhwqnuYkqbuoGo6wYGIZf1I9nlFQZQ5DptX1k)

 



Tessellation factor: polygon division factor. Values are between 0 (original geometry) and 64.

![tessellation_Factor.jpg](https://lh6.googleusercontent.com/aLTTl1bgkDcvTu6qhhKw_MWK0lCe_otK6p0-4IAMNXWf0Q5NN_WouuF7sEpz_bYOSaDg5kqiU5nZvXuFzn18vSrBeABPdmlrlV9upmGdnEOfBsG9rR4IO4mbC0E3R4ahoyc9cSce)

Start fade distance: Distance in meter where the tessellation start to reduce.

 

End fade distance: Distance in meter where the tessellation factor is 0.

 

Triangle size: manage polygon division compared to screen size in pixels.

 

Shape factor: Only available with phong tessellation mode. It is the strength of phong tessellation shape (lerp factor between 0 and 1).

 

 

## 

## 2.3 Vertex animation.

![img](https://lh6.googleusercontent.com/_LQqLWmq-ExU3M3_yuLTuKLmX9MwROHdX_sxsvCeKDcwpLgI8gMxqvubuiQ_c-pImg2NWql2vv2cKv0-R4yfTP-KQFb3RrZ8mEpoRovAeDkdxIjSTgUxdL5GN9WlGB0OphhMYTiO)

 

Enable wind: Activate the wind interaction. A wind asset with the associate script should be in the scene.

 

Initial Bend: increase or decrease the bend effect depending about the wind setting.

 

Stiffness: increase or decrease the stiffness from bottom to top.

 

Drag: manage the move amplitude.

 

Shiver drag: manage the shiver amplitude. The vertex alpha modulates the amplitude.

 

Shiver directionality: handle to manage shiver directionality between mesh normal (0) and wind direction (1).

 

## 2.4 Inputs.

![img](https://lh3.googleusercontent.com/av1PJt9p4mpuH8rF9K-_9Yer055sEO1ZgEGqI8Y3NlR8fm9V0haVleffKU9sLIi5tMATowiu1oDp3wUsYGkzpdC47anDh81xqGPYvzZ74l7ZV3St82EtURskYa22E-6jhxMntdXp)

 

Layer Count: handle to set between 2 and 4 layers.

 

Layer Mask: Texture to manage layers visibility. R for layer 1, G for layer 2, B for layer 3, alpha for main layer.

 

BlendMask UV Mapping: Set the mask UV channel.

- Tiling: Mask UV tiling.
- Offset: Offset the Mask UV.

 

Vertex color mode: use vertex color combine to layer mask to manage layers visibility.

None: vertex color unused.

Multiply: for each channel multiply the vertex color value with the mask. Default mask value is 1.

Add: for each channel middle grey (128, 128, 128) is the mask value. Other values override the mask value. 0 to 127 is used to modulate the erasure and 129 to 255 is used to modulate the add.

 

Main layer influence: allow layers 1, 2 and 3 to be influenced by the main layer. Albedo, normal and height influences can be set into each layer.

 

 

 

Use Height Based blend: activate blending via height map. 

![heightBasedBlend.jpg](https://lh4.googleusercontent.com/breBrTV9-Dforb5P6CFFn2e_13-vEYuWkQGKWH83D5wfkV7ZghRjf3v8EfgJzxjsTYnuF5mqSpetJ1CDZz8Ogc4-7sYkGaset3qbrvnpqWVC5apWOIksnHBRj6Dlzg2WDd9nGlq1)

The use of height base blend allows the height blend transition to manage the layer distance transition. The unit is in world unit between 0 and 1.

![img](https://lh6.googleusercontent.com/GL67UBCTOSD_2T7pTDaOgf0BLRyQWu2jOJTZkMOGzKCRpIghvZOBJN80hrytgHlzgTJWB3qzQBIYwyqwHamBYMQL6D9nCNcbDGLM_s3ELsr8VfeweKOZpUBmdmdzsJzdQdjEq3Je)

 

Lock layers 123 tiling with object scale: the object scale is multiplied to the material tiling to keep the height map appearance.

 



Material References:

![img](https://lh3.googleusercontent.com/KmOdniH7XYIsSBLtzAkZnS4nWnnzMB1mtXrQYOebDuVjZDr_eSSbvDTJCnmHShGUYmg3YI3vK_6chtYy0Hemo5275FLi9tI15jdHxqDpFlIg-jDi4ZtDK59F8QuxPC0ZnDyomvIy)

It is the list of the materials used in the layered shader. If a material source has been modified, it can re-synchronize totally or without original UV mapping settings.

 

Main layer: It is the undermost layer. It can influence upper layers with albedo, normal and height.

 

Layer 1, 2, 3: They are rendered on top of the main layer. The layer 3 is rendered at last on top.

 

# 3 Layers.

## 3.1 Main layer.

![img](https://lh6.googleusercontent.com/p9r_6A21bJ_6FRyDaRx7RkCmsEApXMW0iRDoVZulNJGGDd3enZ8Vzw9d0tSIL5lAlTHILBOHRfeb9EMa3KOykteGRvVW_avHWCtX4GdIGctt_jbc80b3pxkmHFVWn3MhU7G8ux6g)

 

### 3.1.1 Layering Options:

Layer influence Mask: When the main layer influence is active, a mask can be add to define influence areas (white = 100%, black = 0%).

 

Height Offset: Offset the layer without offset the geometry.

 

 

### 3.1.2 Inputs:

 

Base color + opacity: assign the albedo texture. The texture is multiplied by the material color. If no texture is assigned, the color is the base color. Texture alpha is used as alpha.

 

Metallic: this handle allows to set if a material is metallic or not. If a mask map is assigned, it is a  factor multiply to the map value.

 

Smoothness: this handle allows to set if a material is glossy or rough. If a mask map is assigned, it is a factor multiply to the map value.

 

Mask map: it is a composited map. It has to be imported as a linear texture.

​    Red channel: Metallic mask.

Green channel: Ambient occlusion.

Blue channel: Detail map mask.

Alpha channel: Smoothness map.

 

Normal map space: Normal can be set as tangent space or object space.

 

Normal Map: assign the normal map. The handle can be used to refine normal strength.

 

Bent normal map: The bent normal is used to manage an occlusion with the indirect diffuse lighting (lightmap/lightprobe) - Cosine weighted Bent Normal Map (average unoccluded direction). Supported format: BC7, BC5, DXT5(nm). 

 

Height Map: The red channel of the map assign is used as height map. It has to be imported as a linear texture.

 

- Parametrization: Min/Max or Amplitude.

​    ![img](https://lh6.googleusercontent.com/nnDuOfhIlaCKvGc3Sm7haeMUx145e5hmydcad0EN-m7qC4qjbqRni_Dzyg-2Qx8s3O9lup3I54zW60XTMDwMuiOpso9Djz8DNwuLn-gv4Wai13X4atyTQ9U6tMCd_y3kHqhHspLo)

 

Min: the lower value in the height map.

Max: the bigger value in the height map.

The value 0 match with the base mesh surface.

Offset: This value offset in world space the height map base.

 

 

![img](https://lh4.googleusercontent.com/TOYIRRb-7D16BKW7YGXiI-rn63ULF4ZDKLiPgPfTeoT1Ix5AAYcdn2D9KYkZHyVknKKlmL4_zG64Hu61rCsVY1n07EY4a8QSgzYC_MY6x1WkQinfCA8pWfaCO36ERh3vxmKffQ8F)

Amplitude: It is the range between the min and the max value. The base is always at the middle of this value.

Base: It is the base position in the height texture space. (0= 0, 0.5= 128, 1= 255).

Offset: This value offset in world space the height map base.

 

 

 

Base UV mapping: Define UV set between UV0, UV1, UV2, UV3, planar and triplanar. Pay attention about triplanar because it is really expensive. In case of planar and triplanar a world scale is used to define the world size of the material (Ex: 1= 1 meter, 0.5= 2 meters,...).

 

Tiling: apply a tile factor to x/y.

 

Offset: apply a UV position offset to x/y.

 

 

### 3.1.3 Detail Inputs:

 

The visibility of the detail texture is managed by the blue channel of the mask map.

 

Detail map: It is a blend map. Each channel is used to store informations about the detail map.  It has to be imported as a linear texture.

 

​    Red channel: Albedo in grey.

​    Green channel: Green channel of the normal map.

​    Blue channel: Smoothness.

​    Alpha channel: Red channel of the normal map.

 

Detail UV mapping: Define UV set between UV0, UV1, UV2, UV3. If planar or triplanar UV are applied to the material, the detail texture uses too planar or triplanar UV.

Nb: lightmaps use UV1.

Lock to Base Tiling/Offset: If it is activated, the detail map tiling is multiply by the material tiling. In this case the tiling ratio between the material and the detail map is conserved.

 

Tiling: apply a tile factor to x/y.

 

Offset: apply an UV position offset to x/y.

Detail AlbedoScale: handle to manage Albedo overlay of the detail map. Factor between 0 and 2.

 

Detail NormalScale: handle to manage Normal add of the detail map. Factor between 0 and 2.

 

Detail SmoothnessScale: handle to manage smoothness overlay of the detail map. Factor between 0 and 2.

 

 

## 3.2 Layer 1, 2, 3.

 

It is the same setting than the main layer except for Layering options

 

![img](https://lh6.googleusercontent.com/voC5SPX9YkXog_hc56H2DpfReQNqoi4snwWC4RsaT1pLTTkrTgIV2_3KUtmuuuS9b6TIFh3zhc0aOoEO-Gittsl4LdKrXvwiQnCL8JTt1MV430qsuGyhh8f34o2pUP-dvTNoKaHG)

 

Use Opacity map as Density map: Base color alpha channel is used as opacity threshold instead of standard opacity.

 

The vertex color modulates the threshold. The effect depends if the vertex color mode is set to multiply or to add (See: [2-4 Inputs - Vertex color mode](https://docs.google.com/document/d/1-0VZ0IaM5l-mZ4T7s5j55_yvEcYfo4Qso8cYKfspMsQ/edit#heading=h.vjd3knt382ta)).

 

 

0= full opacity, 1= full density.



Example with multiply mode (mask value is 1 by default):

 

![Density.jpg](https://lh6.googleusercontent.com/ioImG7axFIeV1lkkMbQNdTUamUp6Loow_InQJcNJuuIsiM6eBC4LH56H4V_0ovOWdxe3qhcf0m7BTBopcJXJw6--CTQvH3ylu8_8f-hzsuybUCwvqyhLLmLY_oQYEvohlsp-6SGy)

 

BaseColor influence: Variance of the current layer is add to main layer.

 

Normal influence: main layer Normal map is added.

 

Heightmap influence: main layer Height map is added.

# 4 Emissive Inputs.

![img](https://lh6.googleusercontent.com/VpQ6wT8CqOnyjGtvGnTO-IZCgZXcZLakZPPhuatZTvHZ8ABln5T49KGxbvNqE28VNsDu_oa9JpA0vYNyNEKSnKwoO5aFzQA-oJev3uCugKYy77DeHj2URyREjModiUnAX_Q275QI)

 

Emissive Color: This texture is used as emissive. This texture is multiplied by the color. Default value is 1 if no texture is assigned and in this case only the color picker affects the emissive color.

 

Base UV mapping: Define UV set between UV0, UV1, UV2, UV3, planar or triplanar.

 

Tiling: apply a tile factor to x/y.

 

Offset: apply an UV position offset to x/y.

 

Emissive intensity: Manage the power of the emissive effect.

 

Albedo Affect Emissive: When activated the albedo is multiplied with the emissive color.

 

# 5 Advanced options.

Enable GPU instancing: Enable it to create instance of similar objects with this material. GPU instancing and static batching can’t be used at the same time, GPU instancing has the priority.

 

Enable Specular Occlusion from Bent normal: Enable it to use the Bent normal instead of the Ambient Occlusion map to manage the specular occlusion.

 

 