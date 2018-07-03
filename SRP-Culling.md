# Culling
Culling is the process of figuring out what to render on the the screen.

In Unity Culling encompasses:

* Frustum culling: Calculating the objects that exist between the camera near and far plane.
* Occlusion culling: Calculating which objects are hidden behind other objects and excluding them from rendering. For more information see the Occlusion Culling docs.

When rendering starts, the first thing that needs to be calculated is what to render. This involves taking the camera and performing a cull operation from the perspective of the camera. The cull operation returns a list of objects and lights that are valid to render for the camera. These object are then used later in the render pipeline.

## Culling in SRP
In SRP, you generally perform object rendering from the perspective of a Camera. This is the same camera object that Unity uses for built-in rendering. SRP provides a number of API’s to begin culling with. Generally the flow looks as follows:

```C#
// Create an structure to hold the culling paramaters
ScriptableCullingParameters cullingParams;

//Populate the culling paramaters from the camera
if (!CullResults.GetCullingParameters(camera, stereoEnabled, out cullingParams))
    continue;

// if you like you can modify the culling paramaters here
cullingParams.isOrthographic = true;

// Create a structure to hold the cull results
CullResults cullResults = new CullResults();

// Perform the culling operation
CullResults.Cull(ref cullingParams, context, ref cullResults);
```

The cull results that get populated can now be used to perform rendering.