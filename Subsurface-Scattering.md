# What is Subsurface Scattering?

By definition, **Subsurface Scattering (SSS)** is light transport within the participating media under the surface.
In practice, it makes organic materials such as skin look smooth and natural rather than rough and plasticy.
The **HD Render Pipeline (HDRP)** implements the **SSS** effect using a screen-space blur technique.

**SSS** is also responsible for the translucent look of back-lit objects that allow a portion of light to penetrate (transmit through) them. For certain types of objects, performing the blur pass may not make a large visual difference. Therefore, the **HDRP** implements two material types: the **Subsurface Scattering** material type implements both the screen-space blur and transmission (the latter can be disabled), while the **Translucent** material type only models transmission.

You can learn more about our implementation from the slides of our [Siggraph 2018 presentation](http://advances.realtimerendering.com/s2018/Efficient%20screen%20space%20subsurface%20scattering%20Siggraph%202018.pdf).

# Enabling Subsurface Scattering

**SSS** can be toggled in the **HDRP Asset**.

![SSS Settings in the HDRP Asset](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/9f95453c7f7a178151c327becbd7f8b01ca6544e/com.unity.render-pipelines.high-definition/Documentation~/Images/sss_hd_asset.png)

- In your **HDRP Asset** under **Supported Features** check the **Subsurface Scattering** option.
- Optionally, just below, you may choose to **Increase the SSS Sample Count**. This can potentially reduce the amount of visual noise (caused by undersampling) produced by the blur pass at roughly 2.5x the cost, so make sure you can afford it.
- Still in the **HDRP Asset**, locate the **Default Frame Settings**. Under the **Lighting Settings**, make sure that both **Subsurface Scattering** and **Transmission** are enabled.

Most **SSS**-related settings are stored in a **Diffusion Profile**. **Diffusion Profile Settings** is an asset which contains a set of 15 diffusion profiles, which you can edit and assign to your materials.

To create **Diffusion Profile Settings**, navigate to the **Project** tab and click **Create -> Rendering -> Diffusion Profile Settings**. Afterwards, make sure to assign it to the **HDRP Asset**.

# Adding Subsurface Scattering to Your Material

The first step is to change the type of your material. It can be done by simply changing the material type to **Subsurface Scattering** or **Translucent**.

![Material Type UI](https://github.com/EvgeniiG/ScriptableRenderLoop/blob/40aec8b63eb17104819a17d0038af99ef56777cd/com.unity.render-pipelines.high-definition/Documentation~/Images/sss_material_type.png)

For the **Subsurface Scattering** material type, it's also possible to completely disable **Transmission** using the checkbox below.

# Customizing the Behavior of Subsurface Scattering

Changing the material type to **Subsurface Scattering** or **Translucent** adds several new parameters to the material UI.

![SSS Material Inputs](https://github.com/EvgeniiG/ScriptableRenderLoop/blob/ae0788dcf87c1276967929def5343fa7bf7112e9/com.unity.render-pipelines.high-definition/Documentation~/Images/sss_mat_inputs.png)

These parameters are:

- **Subsurface Mask** controls the strength of the blur effect. Texels with the value of 1 correspond to full strength, while using the value of 0 disables the **SSS** effect. It also acts as a multiplier for the texels of the **Subsurface Mask Map** (discussed below).
- **Subsurface Mask Map** is a greyscale texture with values in the [0, 1] range (using the red channel) controlling the strength of the blur effect. Texels with the value of 1 correspond to full strength, while using the value of 0 disables the **SSS** effect.
- **Thickness Map** is a greyscale texture with values in the [0, 1] range (using the red channel) controlling the strength of the transmission effect. It corresponds to the average thickness of the mesh at the location of the texel. Thicker objects transmit less light.
- **Thickness Remap** allows you to remap the values in the **Thickness Map** from the [0, 1] to the smaller [Min, Max] range where (Min < Max) and both Min and Max are themselves in the [0, 1] range.
- **Diffusion Profile** and its configuration is the primary factor diving the behavior of **SSS**. You can select one of 15 profiles from the **Diffusion Profile Settings** asset, or select **None**, which will effectively disable the **SSS** effect. Clicking **GoTo** will take you to the editor of the currently selected **Diffusion Profile**.

# Configuring the Diffusion Profile

Each diffusion profile contains several parameters.

![Diffusion Profile UI](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/5270e4750e994e3bd9bdd26c89d6a748bd5ce39e/com.unity.render-pipelines.high-definition/Documentation~/Images/sss_diffusion_profile.png)

- **Name** - the name of the parameter allows you to easily identify the profile when assigning it to the material.
- **Scattering Distance** - this is a set of three unitless distances (one per color channel) which specify how far light travels under the surface. The effective maximum radius of the effect (in millimeters) is displayed as **Max Radius** just below. It affects the color bleeding/blurring behavior of **SSS** as well as the color tint of **Transmission**.
- **Index of Refraction (IOR)** specifies the reflective behavior of material. Larger values increase the intensity of specular reflection at the normal angle of incidence (looking in the direction perpendicular to the surface). The IOR of skin is typically around 1.4. A list of IOR values of common materials can be found [here](https://pixelandpoly.com/ior.html).
- **World Scale** allows you set the size of the world unit in meters. By default, the **HDRP** assumes that 1 unit = 1 meter. Note that this property only affects the **SSS** pass.
- **Texturing Mode** controls when the albedo (diffuse color) texture is applied. Selecting the **Post-Scatter** texturing mode tells the renderer to apply the albedo after the **SSS** pass, which means that the contents of the texture are not blurred. This mode should be used for scanned data and photographs that already contain some blur due to **SSS**. **Pre- and Post-Scatter** texturing mode effectively blurs the albedo, which can result in a softer, more natural look, which is desirable in certain cases.
- **Transmission Mode** selects a particular implementation of transmission. **Thick Object** should be used for geometrically thick meshes, and **Thin Object** should be used for thin double-sided geometry (cards).
- **Transmission Tint** is a multiplier for the color of transmitted/translucent lighting. Unlike the **Scattering Distance**, its effect does not change depending on the distance (or the thickness).
- **Thickness Remap** is the second thickness remap from the [0, 1] range to the specified range in millimeters. The actual values are displayed by the **Min-Max Thickness** fields just above.

# Working with Different Thickness Modes

The primary difference between the two thickness modes is the use of shadows.
If your light is unshadowed (or you disable shadows), both modes will look exactly the same, and derive the appearance from the **Thickness Map** and the **Diffusion Profile**.
Once you enable shadows, you are likely to see a difference if your object uses thick geometry. The **Thin Object** mode is likely to self-shadow, which can cause it to appear completely black. The **Thick Object** mode will derive the thickness from the shadow map, take the largest value between the "baked" thickness and the "shadow" thickness, and use this to evaluate transmittance.

Since you cannot control the distance derived from the shadow map, one way to approach the **Thick Object** mode would be to enable shadows, adjust the **Scattering Distance** until the overall transmission intensity is in the desired range, and then use the **Thickness Map** to mask any shadow mapping artifacts.