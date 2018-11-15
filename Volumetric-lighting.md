**[Atmospheric Scattering](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Atmospheric-Scattering)** in the HD Render Pipeline (HDRP) is composed of several components. One of them is the **Volumetric Fog**.

The Volumetric Fog is rendered by the Volumetric Lighting system. The HDRP implements a **unified lighting system**, which means that all scene components (lights, as well as opaque and transparent objects) interact with the fog.

Please note that the Volumetric Lighting system does not yet support area lights.

# Enabling Volumetric Lighting

- In your HDRP Asset under **Supported Features** check the **Volumetrics** option.
- Optionally, just below, you may choose to **Increase the Resolution of Volumetrics**. Volumetric lighting is an expensive effect, and this option can increase the cost of the feature by up to 8x, so make sure you can afford it.
- Still in the HDRP Asset, locate the **Default Frame Settings**. Under **Lighting Settings**, make sure that both **Atmospheric Scattering** and **Volumetrics** are enabled.
- Optionally, just below, you may choose to **Enable Reprojection for Volumetrics**. Similarly to the **Temporal Antialiasing**, this option improves the quality of lighting by taking previous frames into account. Currently, this option is not compatible with dynamic lights, so you may encounter ghosting artifacts behind moving lights. Additionally, you may encounter flickering shadows for high values of the **Anisotropy** parameter.

![Volumetric Lighting in the HDRP Asset](https://github.com/EvgeniiG/ScriptableRenderLoop/blob/abb57ca719b4bae4e0eb284f57c5cfc6b223f027/com.unity.render-pipelines.high-definition/Documentation~/Images/vl_asset_settings.png)

# Adding Fog to Your Scene

- In your scene or multi-scene setup (several scenes are loaded) : 

  - if you have a Gameobject with a **Volume component** on it containing a **Visual Environment**, make sure the **Fog Type** is set to **Volumetric Fog**. 
  - if you don't have any **Volume** in your scene, in the **Hierarchy view**, click the **Create** button and then click **Rendering / Scene Settings**. This will create a Gameobject called **Scene Settings** containing a **Volume** with a **Visual Environment**. Select **Scene Settings** and in **Visual Environment** set the **Fog Type** to **Volumetric Fog**.


| Volumes and Visual Environment                               |
| :----------------------------------------------------------- |
| There is usually only one volume that contains **Visual Environment** and it is set as **Global** in order to keep the same **Sky Type** and **Fog Type** everywhere in the scene or multi-scene setup. It is possible to use **local Volumes** with **different Sky Type or Fog Type** but there will be **no transition** between the different sky types or fog types so this is best used on camera cuts. |

At this point, Volumetric lighting is enabled but has **no visible effect because the default air density is very low**. This is expected, and you need to tweak the volumetric lighting settings as explained in next section.

# Tweaking volumetric lighting settings

The Volumetric lighting settings can be tweaked through 2 Volume components :

- **[Volumetric Fog](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/HDRP-Volumetric-Fog)** this component allows you to control the settings used for the simulation of the light scattering through the volume
- **[Volumetric lighting controller](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/HDRP-Volumetric-lighting-controller)** this component allows you to control the space covered by the volumetric lighting simulation and how the precision of the simulation is distributed in that space.

# Specific light parameters

The light component contains some settings that are especially useful when Volumetric lighting is enabled and some that only affect Volumetric lighting.

See in the [Light component page](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/HDRP-Light-Component) : light size, volumetric dimmer, volumetric shadow dimmer.