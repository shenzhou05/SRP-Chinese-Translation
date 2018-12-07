The Volume framework is a generic localized parameter interpolation framework. It allows users to define sets of global parameters that can be interpolated depending on the camera position. For example, users can change the mood of the scene by altering the fog color and density depending on the player position.

The **Volume** component can be added to any game object, the camera itself included. But it's generally a good idea to create a dedicated object for each volume. The Volume component itself does not contains values to interpolate. Instead users will add [VolumeComponents](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/VolumeComponent). **VolumeComponents** are user defined structures containing the actual values to interpolate. The **Volume** has a few parameters allowing to control how it interacts with other volumes. In practice, a scene will contain many Volumes and based on these parameters, the system will determine the final interpolated values for each VolumeComponent.

<p align="center">
[[/images/quickstart-2.png|Quickstart 2]]
</p>

| Property           | Description                                                  |
| ------------------ | ------------------------------------------------------------ |
| **Is Global**      | The Volume has no boundaries and will be applied to the whole scene. |
| **Blend Distance** | Outer distance to start blending from. A value of 0 means no blending and the volume overrides will be applied immediately upon entry. |
| **Weight**         | Multiplier applied to the contribution of the volume computed from its position and blend distance. Allows user to give more or less importance to specific volumes |
| **Priority**       | Value used to determine which volume to use when volumes have the same contribution. Higher priorities will be used first. |
| **Profile**        | Asset containing the Volume Components holding parameters to interpolate. |

When a volume is local, it needs a collider or trigger component attached to it to define its boundaries. Any type of 3D collider will work, from cubes to complex convex meshes but we recommend you use simple colliders as much as possible, as meshes can be quite expensive to traverse. Local volumes can also have a `Blend Distance` that represents the outer distance from the volume surface where blending will start.

The profile is an asset that contains all the VolumeComponents. It can be assigned like any other asset or a new one can be created or cloned using the provided buttons.

At runtime, the system will traverse all Volumes enabled in the scene, and determine based  on position and the above parameters, a contribution for each volume. All volumes with a non zero contribution will then be used to interpolate the values from their VolumeComponents. In practice, not all Volumes will contain the same VolumeComponents. For example, only one may hold the Sky VolumeComponent but several can have the Fog VolumeComponent. In this case, only the existing VolumeComponent will contribute for a given VolumeComponent type.