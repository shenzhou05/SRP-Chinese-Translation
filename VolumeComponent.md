**VolumeComponents** are user defined structures containing values that will be interpolated using the [Volume](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Volumes) framework.

Here is an example of such a Volume Component:

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/VolumeComponent.png)

Each field has an override checkbox on its left, you'll need to toggle the settings you want to override for this volume before you can edit them. You can quickly toggle them all on or off by using the small `All` and `None` shortcuts at the top left. This override checkbox allows users to partially override values for a given Volume Component type.
For example, users might have setup a global **Volume** containing an Exponential Fog with default values and then local volumes, also with an Exponential Fog but only overriding fog color for this part of the scene.
