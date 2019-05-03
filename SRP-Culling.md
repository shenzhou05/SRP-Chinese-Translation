# 剔除
剔除是搞清楚渲染什么对象到屏幕上的过程。

在Unity中剔除包括：

* 视锥剔除: 计算相机近、远平面之间存在的物体。
* 遮挡剔除: 计算隐藏在其他对象后面的对象，并从渲染中排除这些对象。相关详细信息，请参见遮挡剔除文档。

当渲染开始时，首先需要计算的是要渲染的内容。这涉及到透视像机的拍摄方式与剔除操作。剔除操作返回一个对摄影机渲染有效的列表，列表由对象和灯光组成。这些对象随后将在渲染管线中使用。

## SRP中的剔除
在SRP中，通常在透视相机中执行物体渲染。这与Unity内建渲染管线的相机对象相同。SRP提供了许多与剔除相关的API。通常流程如下：

```C#
// 创建一个结构体来保存剔除参数
ScriptableCullingParameters cullingParams;

// 在相机中填充剔除参数
if (!CullResults.GetCullingParameters(camera, stereoEnabled, out cullingParams))
    continue;

// 如果您想要修改剔除参数
cullingParams.isOrthographic = true;

// 创建一个结构体来保存剔除结果
CullResults cullResults = new CullResults();

// 执行剔除操作
CullResults.Cull(ref cullingParams, context, ref cullResults);
```

被填充后的剔除结果现在可用于执行渲染。