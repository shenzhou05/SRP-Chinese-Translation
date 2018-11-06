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
