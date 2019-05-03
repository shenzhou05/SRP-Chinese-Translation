# 渲染管线上下文
SRP使用延迟执行的概念进行渲染。作为一个使用者，您可构建一个命令列表，然后执行它们。用于构建这些命令的对象称为`scriptablerenderContext`，并作为参数传递给Render函数。

使用一些操作填充上下文后，可以调用“submit”提交所有排序过的Rendering call。这些调用通常是`CommandBuffer`执行指令与srp特定的绘制命令的组合。

例如，使用CommandBuffer清除渲染目标的操作，可由渲染上下午执行：

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
        // does not so much yet :(
        base.Render(context, cameras);

        // 使用配置颜色情况渲染目标
        var cmd = new CommandBuffer();
        cmd.ClearRenderTarget(true, true, m_ClearColor);
        context.ExecuteCommandBuffer(cmd);
        cmd.Release();
        context.Submit();
    }
}
```

渲染上下文可实现效果的更多详细信息，请参见：https://docs.unity3d.com/scriptReference/experimental.rendering.scriptablerendercontext.html