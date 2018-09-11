# Camera

**Cameras** are the devices that capture and display the world to the player. By customizing and manipulating cameras, you can make the presentation of your game truly unique. You can have an unlimited number of cameras in a scene. They can be set to render in any order, at any place on the screen, or only certain parts of the screen.

This is the HD version of the camera used in **Hight Definition Render Pipeline**. You can see it by the component HDAdditionalCameraData. Note that even if displayed here, some camera's elements will be in HDAdditionalCameraData when you use camera in scripts.

You can basically find same elements than in a [Standard Unity Camera](https://docs.unity3d.com/Manual/class-Camera.html) but they have been sorted by their purpose.

(inspector picture here)

|General&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;||
|:----------------------------|:--|
|&nbsp; Clear Mode|As standard [Camera](https://docs.unity3d.com/Manual/class-Camera.html)'s ClearFlag except that have the clear depth option separated for more flexibility. Determine how to clear the currently rendered image.|
|&nbsp; Background Color|As standard [Camera](https://docs.unity3d.com/Manual/class-Camera.html)'s Background except the color is always HDR. Used when no Sky or when **Clear Mode** set to _Background Color_|
|&nbsp; Clear Depth|When enable, depth buffer is cleared. Depth buffer is used to know what part should be rendered over which one.|
|&nbsp; Culling Mask|As standard [Camera](https://docs.unity3d.com/Manual/class-Camera.html)'s Culling Mask. It allows to hide element of scene in non selected layers.|
|&nbsp; Volume Anchor Override|Used to override the application point for Volume. If None, camera position is used. See [Volumes](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Volumes) for additional information.|
|&nbsp; Projection|As standard [Camera](https://docs.unity3d.com/Manual/class-Camera.html)'s Projection. Toggles the camera’s capability to simulate perspective.|
|&nbsp; Size (when Projection is Orthographique)|As standard [Camera](https://docs.unity3d.com/Manual/class-Camera.html)'s Size. It is the projection box size.|
|&nbsp; Field Of view (when Projection is Perspective)|As standard [Camera](https://docs.unity3d.com/Manual/class-Camera.html)'s Field of view. It is the Camera view angle.|
|&nbsp; Clipping Planes|As standard [Camera](https://docs.unity3d.com/Manual/class-Camera.html)'s Clipping Planes. Distances from the camera to start and stop rendering.|
|&nbsp; Rendering Path|Allows to use rendering parameter chosen in current High Definition Render Pipeline Asset or override them for this particular camera. _Custom_ value will add a lot of fields to this component. See [Frame Settings](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Frame-Settings) for more information. Note that the fomer **Allow MSAA** is inside them.|
|**CaptureSettings**||
|&nbsp; Occlusion Culling|As standard [Camera](https://docs.unity3d.com/Manual/class-Camera.html)'s Occlusion Culling.|
|&nbsp; ViewPort Rect|As standard [Camera](https://docs.unity3d.com/Manual/class-Camera.html)'s Viewport Rect. Indicate where on the to write in the rendered image.|
|**Output Settings**||
|&nbsp; Target Display|As standard [Camera](https://docs.unity3d.com/Manual/class-Camera.html)'s Target Display. Allow to choose on which screen display the acquired image.|
|&nbsp; Depth|As standard [Camera](https://docs.unity3d.com/Manual/class-Camera.html)'s Depth. The camera’s position in the draw order.|
|&nbsp; Target Texture|As standard [Camera](https://docs.unity3d.com/Manual/class-Camera.html)'s Target Texture. For storing the acquired image in a **RenderTexture**.|

## Additional info regarding standard camera option
* **Physical Camera**: not yet supported (work on it currently done).
* **Allow MSAA**: could be found now in [Frame Settings](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Frame-Settings). Use a _Custom_ **Rendering Path** to override it for this camera.
* **Allow HDR**: this version of the camera always enable HDR.
* **Allow Dynamic Resolution**: dynamic resolution is not supported at the moment.