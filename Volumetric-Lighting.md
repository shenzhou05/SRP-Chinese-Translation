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
| There is usually only one **Volume** that contains a **Visual Environment** override that is set as **Global** in order to keep the same **Sky Type** and **Fog Type** everywhere in the scene (or multi-scene) setup. It is possible to use **Local Volumes** with different sky and fog types, but the transition between different sky and fog types will be abrupt (**no smooth transition**), so it is best used on camera cuts. |

At this point, the scene contains global volumetric fog. However, the effect is **not visible** because the default fog density is very low. This is expected. You need to tweak fog settings as explained in next section.

# Customizing the Appearance of the Volumetric Fog

The Volumetric lighting settings can be tweaked through 2 Volume components :

- **[Volumetric Fog](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/HDRP-Volumetric-Fog)** this component allows you to control the settings used for the simulation of the light scattering through the volume
- **[Volumetric lighting controller](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/HDRP-Volumetric-lighting-controller)** this component allows you to control the space covered by the volumetric lighting simulation and how the precision of the simulation is distributed in that space.

# Specific light parameters

The light component contains some settings that are especially useful when Volumetric lighting is enabled and some that only affect Volumetric lighting.

See in the [Light component page](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/HDRP-Light-Component) : light size, volumetric dimmer, volumetric shadow dimmer.