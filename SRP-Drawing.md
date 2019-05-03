# 绘制
现在我们有了一组剔除结果，我们可以将它们渲染到屏幕上。

但是这有很多的配置方案，所以需要提前做出一些决策。这些决策大多数由以下因素确定：

* 渲染管线的目标硬件
* 您希望达到的外观细节和感觉
* 您正在做的项目类型

例如，想象一下手机端二维横版游戏和高端第一人称PC游戏。这些游戏有很多不同的约束，所以渲染管线也会有很大的不同。可能做出的一些决策的具体例子：

* HDR vs LDR
* Linear vs Gamma
* MSAA vs 后处理抗锯齿
* PBR材质 vs 简单材质
* 光照 vs 没有光照
* 照明技术
* 阴影技术

在编写渲染管线时做出这些决定，将有助于在编写管线时确定限制因素。

现在，我们将编写一个简单的渲染器，它可以使一些不透明对象不受光照。

## 过滤：渲染队列范围(Bucket)与层

通常渲染对象具有特定的分类，它们可分为不透明的、透明的、次表面的或任意数量的其他类别。Unity使用队列的概念来表示渲染对象的时序，这些队列形成了Bucket（物体的材质决定了哪些物体要被放入）。当渲染函数被SRP调用时，您可以指定使用哪种范围的Bucket。

除了Bucket，Unity默认层也可用于过滤。

当使用SRP绘制物体时，这提供了额外的过滤功能。

```c#
// 获取不透明渲染过滤设置
var opaqueRange = new FilterRenderersSettings();
 
//设置不透明渲染队列范围
opaqueRange.renderQueueRange = new RenderQueueRange()
{
    min = 0,
    max = (int)UnityEngine.Rendering.RenderQueue.GeometryLast,
};
 
//包括全部层
opaqueRange.layerMask = ~0;
```

## 绘制设置：对象如何被绘制
过滤和剔除的使用决定了应该渲染什么，但是之后我们需要确定对象应该如何被绘制。SRP提供了各种选项来配置如何渲染已经通过筛选的对象。用于配置此数据的结构是“DrawRendererSettings”结构体。此结构允许配置许多内容：

* 排序 – 对象渲染的顺序，例如从后到前和从前到后的绘制顺序。
* 逐渲染器标志 – 决定什么“内建”设置应该被Unity传递到着色器，这包括每个对象的灯光探针、每个对象的光照贴图以及类似的设置。
* 渲染标志 – 在批处理、实例化与非实例化过程中应该使用哪种算法。
* 着色器通道 – 当前drawcall应使用哪个着色器通道。

```c#
// 创建绘制渲染设置
// 注意应该填写着色器pass的名字
var drs = new DrawRendererSettings(myCamera, new ShaderPassName("Opaque"));
 
// 开启drawcall实例化
drs.flags = DrawRendererFlags.EnableInstancing;
 
// 将灯光探头与光照贴图数据传递给每个渲染器
drs.rendererConfiguration = RendererConfiguration.PerObjectLightProbe | RendererConfiguration.PerObjectLightmaps;
 
// 正常的不透明物体排序
drs.sorting.flags = SortFlags.CommonOpaque;
```

## Drawing
现在我们有三件事需要发出drawcall请求：

* 过滤结果
* 剔除结果
* 绘制规则

我们现在可以发出drawcall请求！与SRP中的所有内容一样，发出一个drawcall请求作为对上下文的调用。在SRP中，通常不渲染单个网格，而是发出一个调用，一次性渲染大量网格。这减少了脚本执行开销，并允许在CPU上快速执行。

为了发出一个drawcall请求，我们结合了一直在编写的那个函数。

```c#
// 全部渲染器开始绘制
context.DrawRenderers(cullResults.visibleRenderers, ref drs, opaqueRange);

// 提交上下文，这将运算全部的指令队列。
context.Submit();
```

这会将对象绘制到当前绑定的渲染目标中。如果愿意，可以使用CommandBuffer切换渲染目标。