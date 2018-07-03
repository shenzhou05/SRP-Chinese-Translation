# The Rendering entry point
When using SRP you need to define a class that controls rendering; this is the Render Pipeline you will be creating. The entry point is a call to “Render” which takes the render context (described below) and a list of cameras to render.

```C#
public class BasicPipeInstance : RenderPipeline
{
   public override void Render(ScriptableRenderContext context, Camera[] cameras){}
}
```