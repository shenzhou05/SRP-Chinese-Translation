HDRP provides different methods of producing sky within your Unity Project. You can choose which sky type to use for each [Volume](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Volumes) in your Scene by altering the Sky Type property in the Volume’s [Visual Environment](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/HDRP-Visual-Environment) override. HDRP provides the following types of sky:

   - [Procedural Sky](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Procedural-Sky): Produces an environment based on the values you choose within the Procedural Sky Volume component. This is similar to Unity’s built-in render pipeline procedural sky.
   - [Gradient Sky](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Gradient-Sky): Renders a simple sky with three color zones for the top, middle, and bottom sections of the sky.
   - [HDRI Sky](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/HDRI-Sky): Constructs a sky environment based on a cubemap texture you set within the HDRI Volume component.

