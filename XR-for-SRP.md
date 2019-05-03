# SRP中的XR支持
## VR
单通道双边立体渲染在LWRP中得到了充分的支持，在[HDRP](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/VR-in-HDRP)中得到了广泛的支持。此外，LWRP还支持单通道实例和多通道立体渲染。

VR模式仍然必须启用，并在Player Settings中选择相应的VR设备SDK。除此之外，VR的配置使用核心渲染管线（CoreRP）中提供的XR图形配置类进行设置。目前，XR图形配置类提供了一个[XRSettings](https://docs.unity3d.com/2018.3/Documentation/ScriptReference/XR.XRSettings.html)的接口，并将在各种XR SDK子系统可用时，扩展并覆盖它们暴露出的全部knob。

**VR图形设置**

[WIP]

## AR
SRP设置AR的方法与为其他项目设置AR的方法相同。[WIP]
