The HD Render Pipeline Asset

The HD Render Pipeline Asset controls the global rendering settings of your project and creates the rendering pipeline instance. The rendering pipeline instance contains intermediate resources and the render loop implementation. For more information about the rendering pipeline instance, see documentation on [Rendering Pipelines](http://placeholder).

 

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

The HD Render Pipeline Resources Asset stores references to shaders and materials used by HDRP. When a player is build, it will embed all this referenced resources. This is in replacement of the Resources folder mechanism of Unity as multiple render pipeline could be setup in a project and the player must not embed all these resources. 

 

There is always a rende pipeline resource available. The HDRP Asset will reference it automatically on creation. It is possible but not recommended to create a HDRP resource asset with the same command than for HDRP Asset. This asset shouldn’t be modify unless a shader need to be replace by a custom version.

## Diffusion Profile Settings

The Diffusion Profile settings Asset stores Subsurface Scattering and Transmission Control profiles for your project. For further information about the Diffusion Profile Settings asset, refer to documentation on [Subsurface Scattering](http://placeholder).

## Render Pipeline Settings

These settings enable or disable HDRP features in your project. Assets for disabled features will not be loaded in your project and disabled features cannot be enabled during run time. 

 

Use these settings to save memory by disabling features you are not using. 

 

| Property                                      | Function                                                     |
| --------------------------------------------- | ------------------------------------------------------------ |
| Support Shadow Mask                           | Tick this checkbox to enable [Shadowmask](https://docs.unity3d.com/Manual/LightMode-Mixed-Shadowmask.html) in your project. |
| Support SSR (Screen space reflection)         | Tick this checkbox to enable [SSR](https://docs.unity3d.com/Manual/PostProcessing-ScreenSpaceReflection.html). |
| Support SSAO (Screen space ambient occlusion) | Tick this checkbox to enable [SSAO](http://placeholder).     |
| Support Decal Buffer                          | Tick this checkbox to enable Decal Buffer.                   |
| Support Multi Sampling Anti-Aliasing (MSAA)   | Tick this checkbox to enable MSAA.                           |
| MSAA Sample Count                             | Specifies the MSAA sample count. Options are MSAA x2 MSAA x4 and MSAA x8. |
| Support Subsurface Scattering                 | Tick this checkbox to enable Subsurface Scattering.          |
| Support Forward Only                          | Tick this checkbox to only support [forward rendering](https://docs.unity3d.com/Manual/RenderTech-ForwardRendering.html). |
| Support Motion Vectors                        | Tick this checkbox to enable motion vectors.                 |
| Support Stereo Rendering                      | Tick this box to enable [stereo rendering](https://docs.unity3d.com/Manual/SinglePassStereoRendering.html) for VR projects. |
| Enable Ultra Quality SSS                      | Tick this box to enable ultra quality Subsurface Scattering. |

 

## Cookies

Use the Cookie settings to configure the maximum resolution of cookies and texture arrays. Larger sizes use more memory, but result in higher quality images. 

 

| Property           | Function                                                     |
| ------------------ | ------------------------------------------------------------ |
| Cookie Size        | The Maximum Cookie size.                                     |
| Texture Array Size | The maximum Texture Array size                               |
| Point Cookie Size  | The maximum [Point Cookie](https://docs.unity3d.com/Manual/Cookies.html) size |
| Cubemap Array Size | The maximum [Spot Cookie](https://docs.unity3d.com/Manual/Cookies.html) size |

 

## Reflection

Reflection settings <do stuff>

 

| Property                               | Function                                                     |
| -------------------------------------- | ------------------------------------------------------------ |
| Compress Reflection Probe Cache        | Tick this checkbox to compress the Reflection Probe Cache. This does <things> |
| Reflection Cubemap Size                | The maximum resolution of the Reflection [Cubemap](https://docs.unity3d.com/Manual/class-Cubemap.html) |
| Probe Cache Size                       | The maximum resolution of the [Probe Cache](http://placeholder) |
| Compress Planar Reflection Probe Cache | Tick this checkbox to compress the Planar Reflection Probe Cache. This does <things> |
| Planar Reflection Texture Size         | The maximum resolution of the Planar Reflection texture.     |
| Planar Probe Cache Size                | Tick this checkbox to compress the Planar Probe Cache. This does <things> |
| Max Planar Probe Per Frame             | The amount of Planar Probes per frame.                       |

 

## Sky

These settings control skybox reflections and skybox lighting. 

 

| Property                   | Function |
| -------------------------- | -------- |
| Sky Reflection Size        |          |
| Sky Lighting Override Mask |          |

 

## Shadow Atlas Settings

These settings adjust the size of the shadow mask. Smaller values will cause more distant shadows to be discarded, while higher values will lead to more shadows being displayed at longer distances from the camera. 

 

Higher values will use more memory.

 

| Property     | Function                |
| ------------ | ----------------------- |
| Atlas Width  | The Shadow Atlas width  |
| Atlas Height | The Shadow Atlas height |

## Decals

 

| Property      | Function |
| ------------- | -------- |
| Draw Distance |          |
| Atlas Size    |          |

 

## Rendering Passes

![img](https://lh3.googleusercontent.com/FceW7tpqECr28mZXqGyr1P_OrHKaktGJMA2FtHsQQG1aQgx_-RradTAN8xzlpZ4eC-Ia3JPoWydkmMDGvVnfN4L0k4SrFZKJRu1p4TXsT93TeoQb0lRx7x6CWI6k6xGG6OMsQRbQ)

 

These settings enable or disable the rendering passes made my the main camera. Disabling these settings does not save on memory, but can improve performance. 

 

These settings can be enabled or disabled during run time.

 

| Property                      | Function |
| ----------------------------- | -------- |
| Enable Transparent Prepass    |          |
| Enable Transparent Postpass   |          |
| Enable Motion Vectors         |          |
| Enable Object Motion Vectors  |          |
| Enable DBuffer                |          |
| Enable Atmospheric Scattering |          |
| Enable Rough Refraction       |          |
| Enable Distortion             |          |
| Enable Postprocess            |          |

 

## Rendering Settings

![img](https://lh4.googleusercontent.com/o4UxGd5zkgXty8ugYvw1pfHmORnTm_MddUvXOVlGeFlQhHs4O9KVrLf5z9dGCtXcRhJLRvcVlSbPjAvPmihTrjxk9mNpbjeIbOi5QGRblIHNno3_ZD-dtL0BhFY_C_e1nlFAnK5m)

 

Does a >thing<

 

| Property                                    | Function |
| ------------------------------------------- | -------- |
| Enable Forward Rendering Only               |          |
| Enable Depth Prepass With Deferred Renderer |          |
| Enable Async Compute                        |          |
| Enable Opaque Objects                       |          |
| Enable Transparent Objects                  |          |
| Enable MSAA                                 |          |

 

## Lighting Settings

## ![img](https://lh6.googleusercontent.com/WJGKdjjD2SzNWVGc4Qv-diVRIJbksWUC9bFAegEtz8BV8O63S31zby0YoEvuGt050BVOzmBhQrFtoqJpGDLn9qzoa0G6LaAy5PrNJsqqjrJkzbBdRi0SCTZFCPwVkIi6kE2uT7Tn)

 

| Property                     | Function                                                    |
| ---------------------------- | ----------------------------------------------------------- |
| Enable SSR                   | Tick this checkbox to enable Screen Space Reflections       |
| Enable SSAO                  | Tick this checkbox to enable Screen Space Ambient Occlusion |
| Enable Subsurface Scattering | Tick this checkbox to enable Subsurface Scattering          |
| Enable Transmission          | Tick this checkbox to enable Transmission                   |
| Enable Shadow                | Tick this checkbox to enable Shadows                        |
| Enable Contact Shadows       | Tick this checkbox to enable Contact Shadows                |
| Enable Shadow Masks          | Tick this checkbox to enable Shadow Masks                   |

 

## Light Loop Settings

![img](https://lh3.googleusercontent.com/JJC6DDHwT0HTg7AfiDkeQHsvf1X4F-qRQaoBM1D8bq12GpmlE1B90dnPxy_PtYqGHVHq0yjE8FfzZIkC12DpjDP-notLfsFb3ZRRY4zkHvQXG2NWx9aiZpJMXg-f-w0KV4Mn5oQe)

 

| Property                         | Function |
| -------------------------------- | -------- |
| Enable FPTL For Forward Opaque   |          |
| Enable Big Tile Prepass          |          |
| Enable Compute Light Evaluation  |          |
| Enable Compute Light Variants    |          |
| Enable Compute Material Variants |          |

 