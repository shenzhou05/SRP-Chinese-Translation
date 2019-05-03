# 渲染入口
SRP资源控制配置，但渲染过程是由SRP渲染管线实例处理。当开发一个SRP时，您还需要创建这个类，因为这是所有渲染逻辑应该存在的地方。

在最简单的形式中，渲染管线实例非常简单，它只包含一个函数“Render”，最好的方法是认为它是一个空白画布，如果您正在编写自定义渲染管线，您可以自由地以任何您认为合适的方式执行渲染。Render调用接受两个参数

*  `ScriptableRenderContext` 这是一种命令缓冲上下文，您可以在其中对要执行的渲染操作进行排序。
* 一组 `Camera`被认为已启用并应用于渲染。

## 一个基本的管线
[这里](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/SRP-Asset#an-simple-asset-example)的资源示例返回了一个管线实例，该管线实例类可能如下所示。

```C#
public class BasicPipeInstance : RenderPipeline
{
    private Color m_ClearColor = Color.black;

    public BasicPipeInstance(Color clearColor)
    {
        m_ClearColor = clearColor;
    }

    public override void Render(ScriptableRenderContext context, Camera[] cameras)
    {
        // does not so much yet :()
        base.Render(context, cameras);

        // 用配置颜色清空buffer
        var cmd = new CommandBuffer();
        cmd.ClearRenderTarget(true, true, m_ClearColor);
        context.ExecuteCommandBuffer(cmd);
        cmd.Release();
        context.Submit();
    }
}
```

这个管线所做的是执行一个简单的绘制：将屏幕清除为给定的颜色，该颜色是在创建管线实例时由资源设置的。这里有几点需要注意：

* 现有的Unity `CommandBuffers` 被用作许多操作 (本例为`ClearRenderTarget`)
* CommandBuffers是根据传入的上下文安排执行的
* 渲染的最后一步是调用`Submit`，这将在渲染上下文上执行所有命令序列

`RenderPipeline` 的Render函数用于输入自定义渲染的逻辑代码。在这里可以执行剔除、过滤、更改渲染目标和绘制等步骤。这就是构建渲染器的地方！
