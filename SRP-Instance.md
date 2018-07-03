# The Rendering entry point
When using SRP you need to define a class that controls rendering; this is the Render Pipeline you will be creating. The entry point is a call to “Render” which takes the render context and a list of cameras to render.

```C#
public class BasicPipeInstance : RenderPipeline
{
   public override void Render(ScriptableRenderContext context, Camera[] cameras){}
}
```

The `RenderPipeline`'s render function is where you enter the rendering code for your custom renderer. It is here that you perform steps like Culling, Filtering, and Drawing.