# The Rendering entry point
The SRP asset controls configuration, but rendering is handled by the SRP Render Pipeline instance. When developing an SRP you need to also create this class as this is where all the rendering logic should live.

In it's simplest form the Render Pipeline Instance is very simple it just contains a single function "Render", the best way to think of this is that it's a blank canvas where if you are writing a custom render pipeline you are free to perform rendering in any way that you see fit. The render call takes takes two arguments

* A `ScriptableRenderContext` which is a type of command buffer where you can enqueue rendering operations to be performed.
* A set of `Camera`s that are considered enabled and should be used for rendering.

## A basic pipeline
The asset example from [here](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/SRP-Asset#an-simple-asset-example) returned an instance of a pipeline, this pipeline might look like what is below. 

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

        // clear buffers to the configured color
        var cmd = new CommandBuffer();
        cmd.ClearRenderTarget(true, true, m_ClearColor);
        context.ExecuteCommandBuffer(cmd);
        cmd.Release();
        context.Submit();
    }
}
```

What this pipeline does is perform a simple clear the screen to the given clear colour that is set by the asset when the pipeline instance is created. There are a few things to note here:

* Existing Unity `CommandBuffers` are used for many operations (`ClearRenderTarget` in this case)
* CommandBuffers are scheduled against the context that is passed in
* The final step of rendering is to call `Submit` this executes all the queued up command on the render context

The `RenderPipeline`'s render function is where you enter the rendering code for your custom renderer. It is here that you perform steps like Culling, Filtering, Changing render targets, and Drawing. This is where you construct your renderer!