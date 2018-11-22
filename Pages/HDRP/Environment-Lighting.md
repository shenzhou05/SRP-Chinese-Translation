What we refer to as **environment lighting** is the lighting produced by the environment surrounding our unity scene. Most commonly this represents the sky lighting, but it can also represent a different kind of background (light a lighting studio, or any kind of background).

In HD render pipeline, environment lighting is setup through [the Volume framework](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Volumes).

The **Environment lighting** section in the Light settings window is replaced in HD render pipeline by this setup per Volume so that you can smoothly interpolate between different sets of settings for your sky and fog per game area.

The two key concepts for environment lighting are the **visual environment**, and the **baking environment**.

## Visual environment

[Visual Environment](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/HDRP-Visual-Environment) is a Volume component that informs the render pipeline about what type of sky and fog you want to see through your game camera.

Visual Environment is affected by sky global parameters found in the [HDRP asset](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/HDRP-Asset#sky).

**Sky Reflection Size**

This parameter drives the size of the cubemap generated from the sky and used for fallback reflection when no local reflection probes are present. It has no effect on the quality of the sky rendered in the background.

**Sky Lighting Override Mask**

In some cases, users may want to dissociate lighting environment from what is rendered in the background (a typical example is to have a very dark sky at night but have a brighter lighting so that the player can still see).

In order to achieve this, users can define the sky lighting override mask which is a Layer mask. If any volumes are present in this layer then environment lighting will use these volumes instead of those from the main camera. If this mask is set to Nothing or if there are no volume in this mask then lighting will come from volumes setup in the main camera volume layer mask.

HDRP comes with builtin sky types: [HDRI Sky](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/HDRI-Sky), [Gradient Sky](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Gradient-Sky) and [Procedural Sky](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Procedural-Sky). New Sky types can be implemented. For details please refer to the [Customizing HDRP](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Writing-A-Custom-Sky-Renderer) section for instructions on how to add your own Sky Type to HD render pipeline.

## Baking environment

The environment lighting used for light baking is controlled by a component called "**Baking sky**" that informs the Unity Editor which sky to use for **light baking**. This component references a **Volume profile** that just needs to include a **Sky** Volume component which will drive directly the sky used for light baking. This is necessary because the Volume workflow allows you to have different sky settings per area, but if you want to bake **static lighting** the editor needs to know what settings to use for the light baking.

The Volume Profile you reference in the Baking sky component can be a profile assigned to a Volume in your scene (so it matches the sky that is visible at runtime ) or it can be a separate profile if you want to control your environment lighting for light baking separately.

**A typical use case** for using a different profile in the Baking Sky is a HDRI sky that includes the sunlight: You probably want to have a sunlight visible when you play your game so you want your runtime sky to show a HDRI that features a sunlight in it, but you could want to use a different HDRI sky where the sun is erased for light baking because you also have a directional light in your scene that contributes to the lighting as the Sunlight (and thus baking lighting with a HDRI that includes the sun would make the sun contribute to the lighting twice and would look unrealistic).

## Reflections

Note on reflections :

Baked reflection probes will render using the sky settings used in the Baking sky component, as this is consistent with your baking settings.

Realtime reflection probes will render using the sky settings resulting from the Volumes, as this is consistent with what you'll see with your game camera at runtime.

## Adding your own Sky Type

Please refer to the [Customizing HDRP](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Writing-A-Custom-Sky-Renderer) section for instructions on how to add your own Sky Type to HD render pipeline.