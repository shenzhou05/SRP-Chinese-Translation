#Global Shadow Settings

In HDRP, setting up global shadow parameters and parameters for the directional light is a bit different than in the built-in legacy pipelines. All these shadow settings use the Volume system so that users can easily change them depending on the camera position without the need for scripting.

Note that all parameters explained below are actually not interpolated. The reason is that most of those, if interpolated would cause very bad shadow flickering that would be very distracting in the final image.

The goal of having those parameters in Volumes is to be able to change them at very distinct moment in the game. For example if the player goes from an outside zone to an indoor zone you may want to reduce the shadow max distance and the number of cascades for the directional light. This will allow for level builders to optimize the lighting setups without the need for scripting.

__HD Shadow Settings__

![](../uploads/Main/Copyof Global Shadow Settings_image_0.png)

| Property          | Function                                                     |
| :---------------- | :----------------------------------------------------------- |
| __Max Distance__  | Maximum shadow distance. This is used for both the last directional cascade boundary and for punctual lights. |
| __Cascade Count__ | Number of cascades for the shadow casting directional light  |
| __Split 1__       | Limit between first and second split (expressed as ratio of max shadow distance) |
| __Solit 2__       | Limit between second and third split (expressed as ratio of max shadow distance) |
| __Split 3__       | Limit between third and last split (expressed as ratio of max shadow distance) |



To help setting things up more easily, users can use the contextual menu to directly create a game object named "Scene Settings" and go from there. This game object is already setup with a default HD Shadow Setting inside a global Volume (it also contains fog and sky default settings).

![](../uploads/Main/Copyof Global Shadow Settings_image_1.png)

__Contact Shadows__

Screen space contact shadows can be enabled if a shadow casting directional light is present in the scene. Contact shadows are shadows ray-marched in screen space inside the depth buffer. The goal of contact shadows is to capture small details that cannot be seen in regular shadow mapping algorithm.

Note that this feature is in early development and has not be extensively tested or optimized.

![](../uploads/Main/Copyof Global Shadow Settings_image_2.png)

| Property                  | Function                                                     |
| :------------------------ | :----------------------------------------------------------- |
| __Enable__                | Check to enable the effect                                   |
| __Length__                | Length in world units of the rays used for tracing. It is also the maximum distance at which details can be captured. |
| __Distance Scale Factor__ | Contact Shadows are scaled up with distance to avoid biasing artifacts. Use this parameter to dampen this effect. |
| __Max Distance__          | Distance from the camera in world units at which contact shadows are faded out to zero. |
| __Fade Distance__         | Distance in world units over which the contact shadows are faded out (see Max Distance). |
| __Sample Count__          | Number of samples when ray casting. Increasing this will increase quality at the cost of performance. |



Contact Shadows comparison:

![](../uploads/Main/Copyof Global Shadow Settings_image_3.png)![](../uploads/Main/CopyofGlobal Shadow Settings_image_4.png)
