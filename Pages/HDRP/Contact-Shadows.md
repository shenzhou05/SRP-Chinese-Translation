The Contact Shadows [Volume Override](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Volume-Components) specifies properties which control the behavior of Contacts Shadows. Contact Shadows are shadows that HDRP [ray marches](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Glossary#RayMarching) in screen space inside the depth buffer. The goal of using Contact Shadows is to capture small details that regular shadow mapping algorithms fail to capture.

To use Contact Shadows in your Scene, you must enable them for your Cameras. In the Inspector for your HDRP Asset, go to the **Default Frame Settings** > **Lighting** Section and enable the **Contact Shadows** checkbox. All Cameras now render Contact Shadows unless you override a Camera’s [Frame Settings](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Frame-Settings).

You can enable Contact Shadows on a per Light basis for Directional, Point, and Spot Lights. Tick the **Enable** checkbox under the **Contact Shadows** drop-down in the **Shadows** section of each Light to indicate that HDRP should calculate Contact Shadows for that Light.

Only one Light can cast Contact Shadows at a time. This means that, if you have more than one Light that casts Contact Shadows visible on the screen, only the dominant Light renders Contact Shadows. HDRP chooses the dominant Light using the screen space size of the Light’s bounding box. A Directional Light that casts Contact Shadows is always the dominant Light.

Note: For Mesh Renderer components, setting __Cast Shadows__ to __Off__ does not apply to Contact Shadows.

Contact shadow have a variable cost between 0.5 and 1.3 ms on the base PS4 at 1080p.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/ContactShadows1.png)

| Property                  | Description                                                    |
| :------------------------ | :----------------------------------------------------------- |
| __Enable__                | Enable this checkbox to make HDRP process Contact Shadows for this [Volume](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Volumes). |
| __Length__                | Use this slider to set the length of the rays, in meters, that HDRP uses for tracing. It also functions as the maximum distance at which the rays can captures details. |
| __Distance Scale Factor__ | HDRP scales Contact Shadows up with distance. Use the slider to set the value that HDRP uses to dampen the scale to avoid biasing artifacts with distance. |
| __Max Distance__          | The distance from the Camera, in Unity units, at which HDRP begins to fade Contact Shadows out to zero. |
| __Fade Distance__         | The distance, in Unity units, over which HDRP fades Contact Shadows out when at the __Max Distance__. |
| __Sample Count__          | Use this slider to set the number of samples HDRP uses for ray casting. Increasing this increases quality at the cost of performance. |
| __Opacity__ |   Use this slider to set the opacity of the Contact Shadows. Lower values result in softer, less prominent shadows.   |
