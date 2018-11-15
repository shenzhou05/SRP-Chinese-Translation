**[Atmospheric Scattering](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Atmospheric-Scattering)** in the HD Render Pipeline (HDRP) is composed of several components. One of them is the **Volumetric Fog**.

The Volumetric Fog is rendered by the Volumetric Lighting system. The HDRP implements a **unified lighting system**, which means that all scene components (lights, as well as opaque and transparent objects) interact with the fog.

Please note that the Volumetric Lighting system does not yet support area lights.

# Enabling Volumetric Lighting

- In your HDRP Asset under **Supported Features** check the **Volumetrics** option.
- Optionally, just below, you may choose to **Increase the Resolution of Volumetrics**. Volumetric lighting is an expensive effect, and this option can increase the cost of the feature by up to 8x, so make sure you can afford it.
- Still in the HDRP Asset, locate the **Default Frame Settings**. Under **Lighting Settings**, make sure that both **Atmospheric Scattering** and **Volumetrics** are enabled.
- Optionally, just below, you may choose to **Enable Reprojection for Volumetrics**. Similarly to the Temporal Antialiasing, this option improves the quality of lighting by taking previous frames into account. Currently, this option is not compatible with dynamic lights, so you may encounter ghosting artifacts behind moving lights. Additionally, you may encounter flickering shadows for high values of the **Anisotropy** parameter.

![Volumetric Lighting in the HDRP Asset](https://github.com/EvgeniiG/ScriptableRenderLoop/blob/abb57ca719b4bae4e0eb284f57c5cfc6b223f027/com.unity.render-pipelines.high-definition/Documentation~/Images/vl_asset_settings.png)

# Adding Fog to Your Scene

- In your scene or multi-scene setup (if several scenes are loaded): 
  - If you have a **GameObject** with a **Volume** component containing a **Visual Environment** override, make sure the **Fog Type** is set to **Volumetric**. 
  - If you don't have a **Volume** component in your scene, navigate to the **Hierarchy** view and click **Create** -> **Rendering** -> **Scene Settings**. This will create a **GameObject** called "Scene Settings" containing a **Volume** component with a **Visual Environment** override. Inspect the new **GameObject** and set the **Fog Type** to **Volumetric**.

![Volumetric Fog in the Visual Environment](https://github.com/EvgeniiG/ScriptableRenderLoop/blob/e194c3217ca7989e04f27400f594531f12bf4085/com.unity.render-pipelines.high-definition/Documentation~/Images/vl_visual_env.png)

| Volumes and Visual Environment                               |
| :----------------------------------------------------------- |
| There is usually only one **Volume** containing a **Visual Environment** override that is set as **Global** in order to keep the same **Sky Type** and **Fog Type** everywhere in the scene (or multi-scene) setup. It is possible to use **Local Volumes** with different sky and fog types, but the transition between different sky and fog types will be abrupt (**no smooth transition**), so it is best used on camera cuts. |

At this point, the scene contains global volumetric fog. However, the effect is **not visible** because the default global fog density is very low. This is expected. You need to tweak fog settings as explained in next section.

# Customizing the Global Volumetric Fog

You should start by setting up the global fog. It offers both the best performance and the best quality, so you should prefer to use it over the local fog whenever possible.

The global fog is a height fog. It has two logical components: the region below the **Base Height** is a constant (homogeneous) fog, and the region above the **Base Height** is the exponential fog.

![GLobal Fog Settings](https://github.com/EvgeniiG/ScriptableRenderLoop/blob/2c968f3f3d4b9edb08114c849a0c5ff9d27967d9/com.unity.render-pipelines.high-definition/Documentation~/Images/vl_global_fog.png)

The **Volumetric Fog** component of the active **Volume** controls the appearance of the global fog.

It has several parameters:

- **Single Scattering Albedo** can be thought of as a fog color. It tints lighting scattered by the fog. Note that it will not tint lighting reflected by the objects behind (or within) the fog - reflected lighting only gets dimmer (fades to black) as fog density increases. Technically speaking, this parameter is defined as the ratio of the **Scattering** and **Extinction** coefficients.
- **Base Fog Distance**, or **Base Mean Free Path**, controls the density at the base of the fog. Basically, it determines how far you can see through the fog. At this distance, 63% of background light is lost in the fog (due to absorption and out-scattering)." Technically speaking, it is defined as **1 / Extinction** coefficient.
- **Base Height** is the height of the boundary between the constant (homogeneous) and the exponential fog.
- **Mean Height** controls the rate of falloff of the height fog. Higher values stretch the fog vertically.
- **Global Anisotropy** is an **experimental** parameter applied to **both** global and local fog. It controls the angular distribution of scattered light. 0 is isotropic, 1 is forward scattering, -1 is backward scattering. Note that non-zero values have a moderate performance impact. High values may have compatibility issues with the **Enable Reprojection for Volumetrics** setting.
- **Global Light Probe Dimmer** reduces the intensity of the global **Light Probe** generated by the sky.
- **Max Fog Distance** serves two purposes. First, it controls the distance when shading the skybox (or the background). Second, it determines the range of the **Distant Fog** (discussed below). For optimal results, this distance should be larger than the distance to the far plane of the camera. Otherwise, a discrepancy between the fog applied to the scene objects and the skybox may occur. Note that the far plane of the camera is flat, while we apply fog within a sphere surrounding the camera (hence the name **distance** rather than **depth**). Therefore, the maximum distance to the far plane depends on the field of view, and is usually quite a bit larger than the far plane depth.
- **Enable Distant Fog** activates constant-lit fog behind the volumetrically-lit frustum. The net effect is that the fog will stretch farther in the distance.
- **Color Mode** gives two ways of setting the intensity of lighting of the distant fog.
  - **Constant Color** ensures that the distant fog is uniformly illuminated.
  - **Sky Color** provides a more interesting alternative which depends on the skybox, the view direction and the distance.

The Volumetric lighting settings can be tweaked through 2 Volume components :

- **[Volumetric Fog](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/HDRP-Volumetric-Fog)** this component allows you to control the settings used for the simulation of the light scattering through the volume
- **[Volumetric lighting controller](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/HDRP-Volumetric-lighting-controller)** this component allows you to control the space covered by the volumetric lighting simulation and how the precision of the simulation is distributed in that space.

# Specific light parameters

The light component contains some settings that are especially useful when Volumetric lighting is enabled and some that only affect Volumetric lighting.

See in the [Light component page](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/HDRP-Light-Component) : light size, volumetric dimmer, volumetric shadow dimmer.