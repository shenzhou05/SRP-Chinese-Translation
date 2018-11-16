**[Atmospheric Scattering](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Atmospheric-Scattering)** in the **HD Render Pipeline (HDRP)** is composed of several components. One of them is the **Volumetric Fog**.

The Volumetric Fog is rendered by the Volumetric Lighting system. The HDRP implements a **unified lighting system**, which means that all scene components (lights, as well as opaque and transparent objects) interact with the fog.

Please note that the Volumetric Lighting system does not yet support area lights.

# Enabling Volumetric Lighting

Volumetric Lighting can be toggled in the **HDRP Asset**.

![Volumetric Lighting in the HDRP Asset](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/com.unity.render-pipelines.high-definition/Documentation~/Images/vl_asset_settings.png)

- In your **HDRP Asset** under **Supported Features** check the **Volumetrics** option.
- Optionally, just below, you may choose to **Increase the Resolution of Volumetrics**. Volumetric lighting is an expensive effect, and this option can increase the cost of the feature by up to 8x, so make sure you can afford it.
- Still in the **HDRP Asset**, locate the **Default Frame Settings**. Under **Lighting Settings**, make sure that both **Atmospheric Scattering** and **Volumetrics** are enabled.
- Optionally, just below, you may choose to **Enable Reprojection for Volumetrics**. Similarly to the Temporal Antialiasing, this option improves the quality of lighting by taking previous frames into account. Currently, this option is not compatible with dynamic lights, so you may encounter ghosting artifacts behind moving lights. Additionally, you may encounter flickering shadows for high values of the **Anisotropy** parameter.

# Adding Fog to Your Scene

The **Visual Environment** part of your **Scene Settings** should be configured to use the **Volumetric Fog**.

![Volumetric Fog in the Visual Environment](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/com.unity.render-pipelines.high-definition/Documentation~/Images/vl_visual_env.png)

In order to activate volumetric fog in your scene or multi-scene setup (if several scenes are loaded):

- If you have a **GameObject** with a **Volume** component containing a **Visual Environment** override, make sure the **Fog Type** is set to **Volumetric**. 
- If you don't have a **Volume** component in your scene, navigate to the **Hierarchy** view and click **Create -> Rendering -> Scene Settings**. This will create a **GameObject** called "Scene Settings" containing a **Volume** component with a **Visual Environment** override. Inspect the new **GameObject** and set the **Fog Type** to **Volumetric**.

| Volumes and Visual Environment                               |
| :----------------------------------------------------------- |
| There is usually only one **Volume** containing a **Visual Environment** override that is set as **Global** in order to keep the same **Sky Type** and **Fog Type** everywhere in the scene (or multi-scene) setup. It is possible to use **Local Volumes** with different sky and fog types, but the transition between different sky and fog types will be abrupt (**no smooth transition**), so it is best used on camera cuts. |

At this point, the scene contains global volumetric fog. However, the effect is **not visible** because the default global fog density is very low. This is expected. You need to tweak fog settings as explained in next section.

# Customizing Global Volumetric Fog

You should start by setting up the global fog. It offers both the best performance and the best quality, so you should prefer to use it over the local fog whenever possible.

The global fog is a height fog. It has two logical components: the region below the **Base Height** is a constant (homogeneous) fog, and the region above the **Base Height** is the exponential fog.

The **Volumetric Fog** component of the active **Volume** controls the appearance of the global fog.

![GLobal Fog UI](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/com.unity.render-pipelines.high-definition/Documentation~/Images/vl_global_fog.png)

It has several parameters:

- **Single Scattering Albedo** can be thought of as a fog color. It tints lighting scattered by the fog. Note that it will not tint lighting reflected by the objects behind (or within) the fog - reflected lighting only gets dimmer (fades to black) as fog density increases. Technically speaking, this parameter is defined as the ratio of the **Scattering** and **Extinction** coefficients.
- **Base Fog Distance**, or **Base Mean Free Path**, controls the density at the base of the fog. Basically, it determines how far you can see through the fog. At this distance (in meters), 63% of background light is lost in the fog (due to absorption and out-scattering)." Technically speaking, it is defined as **1 / Extinction** coefficient.
- **Base Height** is the height of the boundary between the constant (homogeneous) and the exponential fog.
- **Mean Height** controls the rate of falloff of the height fog. Higher values stretch the fog vertically. At this height, the initial (base) density is reduced by 63%.
- **Global Anisotropy** is an **experimental** parameter applied to **both** global and local fog. It controls the angular distribution of scattered light. 0 is isotropic, 1 is forward scattering, -1 is backward scattering. Note that non-zero values have a moderate performance impact. High values may have compatibility issues with the **Enable Reprojection for Volumetrics** setting.
- **Global Light Probe Dimmer** reduces the intensity of the global **Light Probe** generated by the sky.
- **Max Fog Distance** serves two purposes. First, it controls the distance (in meters) when shading the skybox (or the background). Second, it determines the range of the **Distant Fog** (discussed below). For optimal results, this distance should be larger than the distance to the far plane of the camera. Otherwise, a discrepancy between the fog applied to the scene objects and the skybox may occur. Note that the far plane of the camera is flat, while we apply fog within a sphere surrounding the camera (hence the name **distance** rather than **depth**). Therefore, the maximum distance to the far plane depends on the field of view, and is usually quite a bit larger than the far plane depth.
- **Enable Distant Fog** activatesthe fog with precomputed lighting behind the volumetrically-lit frustum. The net effect is that the fog will stretch farther in the distance.
- **Color Mode** gives two ways of setting the intensity of lighting of the distant fog.
  - **Constant Color** ensures that the distant fog is uniformly illuminated.
  - **Sky Color** provides a more interesting alternative which depends on the skybox, the view direction and the distance. All lighting comes from the cubemap of the sky.
    - **Mip Fog Near** determines the distance (in meters) at which the least detailed MIP level is used.
    - **Mip Fog Far** determines the distance (in meters) at which the most detailed MIP level is used.
    - **Mip Fog Max Mip** determines what the most detailed MIP level is.

# Adding Local Fog

It is possible to control fog placement in a more fine-grained way by the use of **Density Volumes**.
A **Density Volume** is a an additive volume of fog represented as an oriented bounding box. By default, the fog is constant (homogeneous), but it can be augmented by a **Density Mask** 3D texture. Currently, these 3D textures are limited to the resolution of 32x32x32.

For performance reasons, **Density Volumes** are voxelized. This results in two limitations:

- **Density Volumes** do not support **volumetric shadowing**. If you place a **Density Volume** between a light and a surface, this volume will not attenuate lighting reaching the surface.
- **Density Volumes** are voxelized at a very coarse rate, with (typically) only 64 or 128 slices along the camera's focal axis. This can result in noticeable aliasing at sharp boundary of the volume. In order to hide the problem, you should always have some global fog (if possible). Using a **Density Mask** and a non-zero **Blend Distance** can also make the edge less visually distracting.

To create a **Density Volume**, navigate to the **Hierarchy** view and click **Create -> Rendering -> Density Volume**.

![Density Volume UI](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/com.unity.render-pipelines.high-definition/Documentation~/Images/vl_density_volume.png)

A **Density Volume** has several parameters:

- **Single Scattering Albedo** can be thought of as a fog color. It tints lighting scattered by the fog. Note that it will not tint lighting reflected by the objects behind (or within) the fog - reflected lighting only gets dimmer (fades to black) as fog density increases. Technically speaking, this parameter is defined as the ratio of the **Scattering** and **Extinction** coefficients.
- **Fog Distance**, or **Mean Free Path**, controls the density at the base of the fog. Basically, it determines how far you can see through the fog. At this distance (in meters), 63% of background light is lost in the fog (due to absorption and out-scattering)." Technically speaking, it is defined as **1 / Extinction** coefficient.
- **Size** controls the dimensions of the volume.
- **Blend Distance** creates a linear fade of the specified normalized distance along the specified local axis of the bounding volume. For each axis, it's possible to have two fades, such as left-to-right and right-to-left for the X axis. 0 distance hides the fade, while the distance of 1 results in a fade across the entire volume.
- **Invert Blend** reverses the direction of the fade. Typically, setting all **Blend Distances** to 1 would preserve the center of the volume and fade the edges. Inverting the fade would fade the center and preserve the edges instead.
- **Density Mask Texture** specifies a 3D texture mapped to the interior of the volume. Note that only the alpha channel of the texture is used. The value of the texture acts as a density multiplier. The texture value of 0 would result in a volume of 0 density, and the texture value of 1 would result in the original constant (homogeneous) volume.
- **Scroll Speed** specifies the speed (per-axis) at which the texture should be scrolled.
- **Tiling** specifies the tiling rate (per-axis) of the texture. For example, the rate of 2 means that the texture will be repeated 2 times within the interior of the volume.

# Creating a Density Mask Texture

1. Prepare a 2D texture of size 1024x32 which is a 3D texture of size 32x32x32 with 32 slices laid out one after another.
2. Set **Texture Import Settings**:  
  2.1. Set the **Texture Type** to **Single Channel**.  
  2.2. Set the **Channel** to **Alpha**.  
  2.3. Check **Read/Write Enabled**.  
3. Navigate to **Window -> Rendering -> Density Volume Texture Tool**.
4. Set your texture, and the tool will generate another texture with a different format.
5. Assign the generated texture as the **Density Mask**.

# Specific Light Parameters

The [Light Component](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/HDRP-Light-Component) has several parameters which are particularly useful for volumetric lighting:

- **Light Radius** is useful to simulate fill lighting. It acts by virtually "pushing" the light away from the scene, which effectively performs a remapping of the quadratic falloff curve. As a result, it softens the core of punctual lights. It's a good idea to always use a non-zero value to reduce ghosting artifacts resulting from reprojection.

- **Volumetric Light Dimmer** only affects the fog and replaces the **Light Dimmer** used for surfaces.
- **Volumetric Shadow Dimmer** only affects the fog and replaces the **Shadow Dimmer** used for surfaces.

# Controlling the Range of the Volumetric Fog

Volumetric Lighting is evaluated on a 3D grid mapped to the volumetric frustum. The resolution of the grid is quite low (240x135x64 using the default quality setting at 1080p), so it's important to keep the dimensions of the frustum as small as possible to maintain high quality. It's usually best to use **Distant Fog** for the less visually important background area.

The distance range of the sphere-capped volumetric frustum can be adjusted using the **Volumetric Lighting Controller**.

In order to add the **Volumetric Lighting Controller** to your scene or multi-scene setup (if several scenes are loaded), find or create a **GameObject** with a **Volume** component, and add the **Volumetric Lighting Controller** override.

The **Volumetric Lighting Controller** has several parameters.

![Volumetric Lighting Controller UI](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/master/com.unity.render-pipelines.high-definition/Documentation~/Images/vl_controller.png)

- **Distance Range** determines the distance (in meters) from the camera at which the volumetric frustum begins and ends.
- **Depth Distribution Uniformity** controls how uniform the distribution of slices along the camera's focal axis is. The value of 0 makes the distribution exponential (with the spacing between the slices increasing with the distance from the camera), and the value of 1 results in a uniform distribution.