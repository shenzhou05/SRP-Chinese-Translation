One of HD Render Pipeline **[Atmosphere scattering](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Atmospheric-Scattering)** modes is called **Volumetric fog**.

Volumetric fog works as a **unified volumetric lighting system**. 

When volumetric fog is selected, the renderer considers that **all light scatter in the air** and the user can specify some settings in order to tweak the simulation.

# Enabling volumetric lighting

- In your HD Render Pipeline Asset under **Supported Features** check that **Volumetrics** is enabled.

- Still in the HD Render Pipeline Asset, make sure that in the **Default Frame Settings**, under **Lighting Settings**, **Atmospheric Scattering** and **Volumetrics** are enabled.

- In your scene or multi-scene setup (several scenes are loaded) : 

  - if you have a Gameobject with a **Volume component** on it containing a **Visual Environment**, make sure the **Fog Type** is set to **Volumetric Fog**. 
  - if you don't have any **Volume** in your scene, in the **Hierarchy view**, click the **Create** button and then click **Rendering / Scene Settings**. This will create a Gameobject called **Scene Settings** containing a **Volume** with a **Visual Environment**. Select **Scene Settings** and in **Visual Environment** set the **Fog Type** to **Volumetric Fog**.


| Volumes and Visual Environment                               |
| :----------------------------------------------------------- |
| There is usually only one volume that contains **Visual Environment** and it is set as **Global** in order to keep the same **Sky Type** and **Fog Type** everywhere in the scene or multi-scene setup. It is possible to use **local Volumes** with **different Sky Type or Fog Type** but there will be **no transition** between the different sky types or fog types so this is best used on camera cuts. |

At this point, Volumetric lighting is enabled but has **no visible effect because the default air density is very low**. This is expected, and you need to tweak the volumetric lighting settings as explained in next section.

# Tweaking volumetric lighting settings

The Volumetric lighting settings can be tweaked through 2 Volume components :

- **Volumetric fog :** this component allows you to control the settings used for the simulation of the light scattering through the volume
- **Volumetric lighting controller :** this component allows you to control the space covered by the volumetric lighting simulation and how the precision of the simulation is distributed in that space.

# Specific light parameters

The light component contains some settings that are especially useful when Volumetric lighting is enabled and some that only affect Volumetric lighting.

See in the [Light component page](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/HDRP-Light-Component) : light size, volumetric dimmer, volumetric shadow dimmer.