# Lightweight Pipeline

The Lightweight Pipeline is a Scriptable Render Pipeline available with Unity 2018.1. The LT pipe performs a single-pass forward rendering with light culling per-object with the advantage that all lights are shaded in a single pass. Compared to the vanilla unity forward rendering, which performs and additional pass per pixel light, using the LT pipeline will result in less draw calls at the expense of slightly extra shader complexity.

The pipeline supports at most 8 lights per-object and only supports a subset of vanilla Unity  rendering features. A feature comparison table of Lightweight Pipeline vs stock Unity pipeline can be found [here](https://docs.google.com/document/d/1MgoycUhS9xQKXxbTy1yHt7OCByI10rds3TyRBCSlFmg/).

## How to use Lightweight Pipeline

The Lightweight Pipeline does not work with the Unity stock lit shaders. We have developed a new set of Standard shaders that are located under Lightweight Pipeline group in the material’s shader selection dropdown.


![](images/LightweightGettingStarted2.png)

## Lightweight Pipeline shaders


**Standard (Physically Based):** Single shader with both Metallic and Specular workflows. Light model similar and upgradable from stock Unity standard shaders. BRDF: Lambertian Diffuse + Simplified Cook Torrance (GGX, Simplified KSK and Schlick) Specular

**Standard (Simple Lighting):** Replaces the legacy mobile/lit shaders. It performs a non-energy conserving Blinn-Phong shading. Should be used for games that target devices with very limited bandwidth and that therefore cannot use Physically Based Shading.

**Standard Terrain:** Same as Unity’s stock terrain shader.**(WIP)**

**Standard Unlit:** Unlit shader with the option to sample GI. This replaces Unity’s stock unlit shaders. 

**Particles:** Standard and Standard Unlit particles for lightweight pipeline. Same as Unity’s stock standard particles shaders with the exception of Distortion effect. __(WIP)__

Additionally, all Unity’s unlit stock shaders work with Lightweight Pipeline. That means you can use legacy particles, UI, skybox, and sprite shaders with the pipeline with no additional setup.

When the Lightweight Pipeline is set as the active rendering pipeline all game objects will be created with the correct shaders. This is achieved because the pipeline overrides the default materials in the engine. 

The Lightweight Pipeline also provide material upgraders to upgrade Unity’s stock lit shaders to Lightweight ones. In order to upgrade materials go to *Edit -> Render Pipeline -> Upgrade -> Lightweight.** *Check Upgradable Shaders section below to see what unity stock shaders can be upgraded to Lightweight.

1. **Upgrade Project Materials:** upgrades all materials in the Asset folder to Lightweight materials.

2. **Upgrade Selected Materials** upgrade all currently selected materials to Lightweight materials.

![](images/LightweightGettingStarted3.png)

Material Upgraders

## Lightweight Pipeline Asset

The pipeline asset controls the global rendering quality settings and is responsible for creating the pipeline instance. The pipeline instance contains intermediate resources and the render loop implementation. 

![](images/LightweightGettingStarted4.png)

### Lightweight Pipeline Asset

__Rendering__

| __Render Scale__           | Scales the camera render target allowing the game to render at a resolution different than native resolution. UI is always rendered at native resolution. When in VR mode, VR scaling configuration is used instead. |
| :------------------------- | :----------------------------------------------------------- |
| __Pixel Lights__           | Controls the amount of pixel lights that run in fragment light loop. Lights are sorted and culled per-object. |
| __Enable Vertex Lighting__ | If enabled shades additional lights exceeding the maximum number of pixel lights per-vertex up to the maximum of 8 lights. |
| __Camera Depth Texture__   | If enabled the pipeline will generate camera's depth that can be bound in shaders as _CameraDepthTexture. This is necessary for some effect like Soft Particles.<br/> |
| __Anti Aliasing (MSAA)__   | Controls the global anti aliasing settings.                  |

### Shadows

| __Shadow Type__              | Global shadow settings. Options are NO_SHADOW, HARD_SHADOWS and SOFT_SHADOWS. |
| :--------------------------- | :----------------------------------------------------------- |
| __Shadowmap Resolution__     | Resolution of shadow map texture. If cascades are enabled, cascades will be packed into an atlas and this setting controls the max shadows atlas resolution. |
| __Shadow Near Plane Offset__ | Offset shadow near plane to account for large triangles being distorted by pancaking. |
| __Shadow Distance__          | Max shadow rendering distance.                               |
| __Shadow Cascades__          | Number of cascades in directional light shadows.             |



In order to create a pipeline asset click on *Asset -> Create -> Render Pipeline -> Lightweight -> Pipeline Asset*

![](images/LightweightGettingStarted5.png)

You can create multiple pipeline assets containing different quality levels. Assets can be set by either manually selecting a pipeline asset in Graphics Settings or by setting the *GraphicsSettings.renderPipelineAsset* property.

Graphics Settings with Lightweight Pipeline active

## Creating a new project or using the pipeline with an existing one

Lightweight Pipeline depends on the SRP and Post Processing packages. The packages are downloaded by the Package Manager. Currently, there’s no UI in Unity to download the packages. The packages dependencies have to defined explicitly in a manifest.json file that is located in the UnityPackageManager folder. 


1. Copy the following [manifest.json](https://gist.github.com/phi-lira/8ada999bc71131e4a3ff4e26c935b07f) file to the project’s UnityPackageManager folder. Upon startup or refresh, Unity will download and import the Lightweight Pipeline package and its dependencies. 

2. Set the project to linear color space in Player Settings

3. Create a pipeline asset in *Asset -> Create -> Render Pipeline -> Lightweight -> Pipeline Asset*

4. Set the pipeline asset in Graphics Settings

## Upgradable Shaders

Here’s a list of what Unity stock shaders can be upgraded to Lightweight Pipeline and to what shader they map to.

| Unity vanilla Shader                              | Lightweight Pipeline Shader |
| :------------------------------------------------ | :-------------------------- |
| Standard                                          | Standard (Physically Based) |
| Standard (Specular Setup)                         | Standard (Physically Based) |
| Standard Terrain                                  | Standard Terrain            |
| Particles/Standard Surface                        | Particles/Standard          |
| Particles/Standard Unlit                          | Particles/Standard Unlit    |
| Mobile/Diffuse                                    | Standard (Simple Lighting)  |
| Mobile/Bumped Specular                            | Standard (Simple Lighting)  |
| Mobile/Bumped Specular(1 Directional Light)       | Standard (Simple Lighting)  |
| Mobile/Unlit (Supports Lightmap)                  | Standard (Simple Lighting)  |
| Mobile/VertexLit                                  | Standard (Simple Lighting)  |
| Legacy Shaders/Diffuse                            | Standard (Simple Lighting)  |
| Legacy Shaders/Specular                           | Standard (Simple Lighting)  |
| Legacy Shaders/Bumped Diffuse                     | Standard (Simple Lighting)  |
| Legacy Shaders/Bumped Specular                    | Standard (Simple Lighting)  |
| Legacy Shaders/Self-Illumin/Diffuse               | Standard (Simple Lighting)  |
| Legacy Shaders/Self-Illumin/Bumped Diffuse        | Standard (Simple Lighting)  |
| Legacy Shaders/Self-Illumin/Specular              | Standard (Simple Lighting)  |
| Legacy Shaders/Self-Illumin/Bumped Specular       | Standard (Simple Lighting)  |
| Legacy Shaders/Transparent/Diffuse                | Standard (Simple Lighting)  |
| Legacy Shaders/Transparent/Specular               | Standard (Simple Lighting)  |
| Legacy Shaders/Transparent/Bumped Diffuse         | Standard (Simple Lighting)  |
| Legacy Shaders/Transparent/Bumped Specular        | Standard (Simple Lighting)  |
| Legacy Shaders/Transparent/Cutout/Diffuse         | Standard (Simple Lighting)  |
| Legacy Shaders/Transparent/Cutout/Specular        | Standard (Simple Lighting)  |
| Legacy Shaders/Transparent/Cutout/Bumped Diffuse  | Standard (Simple Lighting)  |
| Legacy Shaders/Transparent/Cutout/Bumped Specular | Standard (Simple Lighting)  |



## Q&A

**What is Scriptable Render Pipeline (SRP)?**

SRP allow developers to write how Unity renders a frame in C#. We will release two builtin render pipelines with Unity: Lightweight Pipeline and HD Pipeline. This allows us to develop each pipeline focused on a set of target platforms, speeding up the development type. By exposing the rendering pipelines to C# we also make Unity less of a black box as one can see what is explicitly happening in the rendering. Developers can use the builtin pipelines we are providing, develop their own pipeline from scratch or even modify the ones we provide to adapt to their game specific requirements.

**How does Lightweight Pipeline compare to Unity builtin pipelines?**

[Here’s a feature comparison table](https://docs.google.com/document/d/1MgoycUhS9xQKXxbTy1yHt7OCByI10rds3TyRBCSlFmg/)

**Who should use Lightweight Pipeline?**

Developers targeting a broad range of mobile platforms, VR and that develop games with limited realtime light capabilities.

**What's the development status of Lightweight Pipeline?**

We are undergoing QA and optimization. Rendering quality and performance is to be improved over the next weeks.

**Where’s the Lightweight Pipeline source? How can I modify it or create my own pipeline?**

Lightweight Pipeline resources are embedded in a package that gets downloaded by the Unity Package Manager. The package contents lie inside an internal Unity cache and they are not visible in the project folder. If you want to have access to Lightweight Pipeline source take a look at the Scriptable Rende Pipeline [github page](https://github.com/Unity-Technologies/ScriptableRenderPipeline/issues). We are working on the API and shader documentation at the moment.

**I found an issue. How should I report it?**

You can report any issues found in our[ github page.](https://github.com/Unity-Technologies/ScriptableRenderPipeline/issues)

​	
