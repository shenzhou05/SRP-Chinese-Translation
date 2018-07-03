# Drawing
Now that we have a set of cull results, we can render them to the screen.

But there are so many ways that things can be configured, so a number of decisions need to be made up front. Many of these decisions will be driven by:

* The hardware you are targeting the render pipeline to
* The specific look and feel you wish to achieve
* The type of project you are making

For example, think of a mobile 2D sidescroller game vs a PC high end first person game. These games have vastly different constraints so will have vastly different render pipelines. Some concrete examples of real decisions that may be made:

* HDR vs LDR
* Linear vs Gamma
* MSAA vs Post Process AA
* PBR Materials vs Simple Materials
* Lighting vs No Lighting
* Lighting Technique
* Shadowing Technique

Making these decisions when writing a render pipeline will help you determine many of the constraints that are placed when authoring it.

For now, we’re going to demonstrate a simple renderer with no lights that can render some of the objects opaque

## Filtering: Render Buckets and Layers
Generally, when rendering object has a specific classification, they are opaque, transparent, sub surface, or any number of other categories. Unity uses a concept of queues for representing when an object should be rendered, these queues form buckets that objects will be placed into (sourced from the material on the object). When rendering is called from SRP, you specify which range of buckets to use.

In addition to buckets, standard Unity layers can also be used for filtering.

This provides the ability for additional filtering when drawing objects via SRP.

```c#
// Get the opaque rendering filter settings
var opaqueRange = new FilterRenderersSettings();
 
//Set the range to be the opaque queues
opaqueRange.renderQueueRange = new RenderQueueRange()
{
    min = 0,
    max = (int)UnityEngine.Rendering.RenderQueue.GeometryLast,
};
 
//Include all layers
opaqueRange.layerMask = ~0;
```

## Draw Settings: How things should be drawn
Using filtering and culling determines what should be rendered, but then we need to determine how it should be rendered. SRP provides a variety of options to configure how your objects that pass filtering should be rendered. The structure used to configure this data is the ‘DrawRenderSettings’ structure. This structure allows for a number of things to be configured:

* Sorting – The order in which objects should be rendered, examples include back to front and front to back.
* Per Renderer flags – What ‘built in’ settings should be passed from Unity to the shader, this includes per object light probes, per object light maps, and similar.
* Rendering flags – What algorithm should be used for batching, instancing vs non-instancing.
* Shader Pass – Which shader pass should be used for the current draw call.

```c#
// Create the draw render settings
// note that it takes a shader pass name
var drs = new DrawRendererSettings(Camera.current, new ShaderPassName("Opaque"));
 
// enable instancing for the draw call
drs.flags = DrawRendererFlags.EnableInstancing;
 
// pass light probe and lightmap data to each renderer
drs.rendererConfiguration = RendererConfiguration.PerObjectLightProbe | RendererConfiguration.PerObjectLightmaps;
 
// sort the objects like normal opaque objects
drs.sorting.flags = SortFlags.CommonOpaque;
```

## Drawing
Now we have the three things we need to issue a draw call:

C* ull results
* Filtering rules
* Drawing rules

We can issue a draw call! Like all things in SRP, a draw call is issued as a call into the context. In SRP you normally don’t render individual meshes, instead you issue a call that renders a large number of them in one go. This reduces script execution overhead as well as allows fast jobified execution on the CPU.

To issue a draw call we combine the functions that we have been building up.

```c#
// draw all of the renderers
context.DrawRenderers(cullResults.visibleRenderers, ref drs, opaqueRange);

// submit the context, this will execute all of the queued up commands.
context.Submit();
```

This will draw the objects into the currently bound render target. You can use a command buffer to switch the render target if you so wish.