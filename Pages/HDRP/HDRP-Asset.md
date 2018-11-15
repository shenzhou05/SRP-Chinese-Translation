The **HD Render Pipeline Asset** controls the global rendering settings of your project and creates the rendering pipeline instance. The rendering pipeline instance contains intermediate resources and the render loop implementation. For more information about the rendering pipeline instance, see documentation on [Rendering Pipelines](http://placeholder).

# Creating a HDRP Asset

A HDRP Asset file is included with the HDRP package and the High Definition Template. 

If you are creating a new project, create your own HDRP asset by following the steps below. Creating a custom HDRP Asset will stop your changes being overwritten by HDRP package updates. 

 

Create a new Render Pipeline Asset in your Unity Project browser at the location you want to create the asset (Caution: You can’t create the asset in Package folder, you need to create in Asset folder).

![img](https://lh6.googleusercontent.com/2bU-kpsMCH0uBM7DrCVKKBYEOAlE7wiUVjdj90Pohz2m162zQacH5OjhcoDAyrTFUib8P8_uLa8SUBoaQATHZa3HUfMYH0xpVe2RVUzz9T18vOaFp2TTiyqPjrpkHXlxO2FfseW6)

 

 

Then in Graphic Settings, setup the HDRenderPipeline Asset

![img](https://lh6.googleusercontent.com/Hq_b6LmrG6Fc9sopHC-AsBqdwnsp0_ZjdttGb7ASalVIL80m9aaEZ8IhkjlIXr6KIwN1lmXuhmrnWXwrViCJ3Q8czNg3AXlFpcwWRO25NaP6olRlPxXAuQ2gqvIBfBXvanX4wTCm)

![img](https://lh5.googleusercontent.com/ve5zgde3jFadz2AaGkvQL5Lhw_ktYd9zYe0cfncAyFG20Qp684LuRqBmx_9k3GKtuSmfhUyU57eqDYW7Y_pV6JExBgZRHKEnSclQrvvJGrg4YvEjhWhGDkBxituYPXkRdMA9sII-)

 

 

 

You can create multiple HDRenderPipeline Assets containing different settings. Assets can be set by either manually selecting a Pipeline Asset in the Graphics Settings window, or by using the [GraphicsSettings.renderPipelineAsset](API Link) property via script. 

 

You must create a new asset for each platform your project will support (PC, Xbox One, Playstation 4, etc) and then assign the relevant Asset when you build your project for each platform. 

![img](https://lh3.googleusercontent.com/AaJXJerlJyziXT7UYqeeHltn40fmpND0ZjsU4uxv9FvevFb4V2hwBJ2yRksOKVB7x9tGFCLiDGc-xXgVGoTws_rUHkG3CY6vIyMd5qF_5oRENJ3vwbdTqTlNm0cc-wVbCZiiLwVd)

## Render Pipeline Resources

The **HD Render Pipeline Resources Asset** stores references to shaders and materials used by HDRP. When a player is build, it will embed all these referenced resources. This is a replacement of the Resources folder mechanism of Unity as multiple render pipeline could be setup in a project and the player must not embed all these resources. 

 

There is always a rende pipeline resource available. The HDRP Asset will reference it automatically on creation. It is possible but not recommended to create a HDRP resource asset with the same command than for HDRP Asset. This asset shouldn’t be modify unless a shader needs to be replaced by a custom version.

## Diffusion Profile Settings

The **Diffusion Profile Settings Asset** stores Subsurface Scattering and Transmission Control profiles for your project. For further information about the Diffusion Profile Settings asset, refer to documentation on [Subsurface Scattering](http://placeholder).

## Render Pipeline Supported features

This list allows you to enable or disable features in your project. Disabled features will not be included in your built game and cannot be enabled at run time.

Use these settings to save memory by disabling features you are not using.  

| Property                                    | Function                                                     |
| ------------------------------------------- | ------------------------------------------------------------ |
| Shadow Mask                                 | Tick this checkbox to enable [Shadowmask](https://docs.unity3d.com/Manual/LightMode-Mixed-Shadowmask.html) in your project. |
| SSR (Screen space reflection)               | Tick this checkbox to enable [SSR](https://docs.unity3d.com/Manual/PostProcessing-ScreenSpaceReflection.html). |
| SSAO (Screen space ambient occlusion)       | Tick this checkbox to enable [SSAO](http://placeholder).     |
| Subsurface Scattering                       | Tick this checkbox to enable Subsurface Scattering.          |
| Increase SSS Sample Count                   | Tick this box to enable ultra quality Subsurface Scattering. |
| Volumetrics                                 | Tick this checkbox to enable Volumetric lighting.            |
| Increase Volumetrics resolution             | Tick this box to enable ultra quality Volumetric lighting.   |
| LightLayers                                 | Tick this checkbox to enable Light Layers.                   |
| Supported Lit Shader Mode                   | Both will render Lit shader using deferred rending for opaque and using forward rendering for transparent. You can use Forward and Deferred modes to force a rendering path. |
| Support Multi Sampling Anti-Aliasing (MSAA) | Tick this checkbox to enable MSAA.                           |
| MSAA Sample count                           | Specifies the MSAA sample count. Options are MSAA x2 MSAA x4 and MSAA x8. |
| Decals                                      | Tick this checkbox to enable Decal Buffer.                   |
| Motion Vectors                              | Tick this checkbox to enable motion vectors.                 |
| Runtime debug display                       | Tick this to include debug shaders in the build.             |
| Dithering cross fade                        | Tick this checkbox to support Dithering cross fade for LOD transitions. |
| Stereo Rendering                            | Tick this box to enable [stereo rendering](https://docs.unity3d.com/Manual/SinglePassStereoRendering.html) for VR projects. |

 

## Default frame Settings

Allows you to choose which rendering passes, rendering settings, lighting settings, and light loop settings are used **by default** in :

- **Cameras**
- **Baked or custom reflection probes**
- **Realtime reflections**

**For instance :** this allows you to enable Postprocess pass by default for cameras but disable it by default for realtime reflections. The default settings can then be overriden on a camera or on a reflection probe.

See the [frame settings page](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Frame-Settings) for more details.



## Cookies

Use the Cookies settings to configure the maximum resolution of cookies and texture arrays. Larger sizes use more memory, but result in higher quality images. 

| Property           | Function                                                     |
| ------------------ | ------------------------------------------------------------ |
| Cookie Size        | The Maximum Cookie size.                                     |
| Texture Array Size | The maximum Texture Array size                               |
| Point Cookie Size  | The maximum [Point Cookie](https://docs.unity3d.com/Manual/Cookies.html) size |
| Cubemap Array Size | The maximum [Spot Cookie](https://docs.unity3d.com/Manual/Cookies.html) size |

 

## Reflections

| Property                               | Function                                                     |
| -------------------------------------- | ------------------------------------------------------------ |
| Compress Reflection Probe Cache        | Tick this checkbox to compress the Reflection Probe Cache.   |
| Reflection Cubemap Size                | The maximum resolution of the Reflection [Cubemap](https://docs.unity3d.com/Manual/class-Cubemap.html) |
| Probe Cache Size                       | The maximum resolution of the [Probe Cache](http://placeholder) |
| Compress Planar Reflection Probe Cache | Tick this checkbox to compress the Planar Reflection Probe Cache. |
| Planar Reflection Texture Size         | The maximum resolution of the Planar Reflection texture.     |
| Planar Probe Cache Size                | Tick this checkbox to compress the Planar Probe Cache.       |
| Max Planar Probe Per Frame             | The amount of Planar Probes per frame.                       |

 

## Sky

These settings control skybox reflections and skybox lighting. 

| Property                   | Function                                                    |
| -------------------------- | ----------------------------------------------------------- |
| Sky Reflection Size        | Sets the resolution of the sky reflection cubemap.          |
| Sky Lighting Override Mask | Sets the layer mask used in order to override sky lighting. |

 

## Shadows 

### Atlas

These settings adjust the size of the atlases where shadow maps are packed. 

The first atlas is used for all punctual lights shadows (spot and point lights) and has the possibility to rescale its shadow maps if too many of them are rendered and would not fit in the atlas. The second atlas is used for directional shadow cascade and doesn't rescale.

| Property        | Function                                                     |
| --------------- | ------------------------------------------------------------ |
| Resolution      | The Shadow Atlas resolution (higher values will use more memory) |
| 16-bit          | Tick this checkbox to use 16-bit format for the shadow map atlas. This is an optimization. |
| Dynamic rescale | Tick this checkbox to enable rescaling for the punctual lights shadow atlas. Punctual lights will see the resolution of their shadow maps scale down with distance to the camera. |

### Max requests

This value restricts the maximum number of shadows that can be computed per frame. 

### Filtering qualities

| Property    | Function                                                     |
| ----------- | ------------------------------------------------------------ |
| Punctual    | Allows you to choose a preset for punctual light filtering quality |
| Directional | Allows you to choose a preset for Directional light filtering quality |

|Preset     |   Algorithm|
|-----------|------------------------|
|Low | PCF 3x3 (4 taps)|
|Medium | PCF 5x5 (9 taps)|
|High | PCSS |

When using **PCSS filtering**, some additional high quality filtering settings become available in the light component.



## Decals

| Property                       | Function                                                     |
| ------------------------------ | ------------------------------------------------------------ |
| Draw Distance                  | Distance at which decals stop being rendered.                |
| Atlas Size                     | Resolution of the decals texture atlas                       |
| Enable Metal and AO properties | Allows Decals to affect Metal and AO material properties. Enabling this option has a performance impact. |