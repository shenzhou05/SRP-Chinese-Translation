# XR Support in SRP
## VR
Single-pass double-wide stereo rendering is fully supported in LWRP and mostly supported in [HDRP](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/VR-in-HDRP). In addition, LWRP also supports single-pass instanced and multi-pass stereo rendering.

VR must still be enabled and a VR SDK chosen in Player Settings. Aside from that, VR settings are configured using the XRGraphicsConfig class provided in CoreRP. Currently, XRGraphicsConfig provides an interface to [XRSettings](https://docs.unity3d.com/2018.3/Documentation/ScriptReference/XR.XRSettings.html), and will be expanded to cover all knobs exposed by various XRSDK Subsystems as they become available. 

**VRGraphicsConfig**

[SECTION WIP]

## AR
AR is set up for SRP the same way it is set up for any other project. [SECTION WIP]
