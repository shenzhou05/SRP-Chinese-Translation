What we refer to as **environment lighting** is the lighting produced by the environment surrounding our unity scene. Most commonly this represents the sky lighting, but it can also represent a different kind of background (light a lighting studio, or any kind of background).

In HD render pipeline, environment lighting is setup through [Volumes](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Volumes) and **volume profiles**.

The **Environment lighting** section in the Light settings window is replaced in HD render pipeline by this setup per Volume so that you can smoothly interpolate between different sets of settings for your sky and fog per game area.

The two key concepts for environment lighting are the **visual environment**, and the **baking environment**.

## Visual environment

**Visual environment** is a Volume component that informs the render pipeline about what type of sky and fog you want to see through your game camera. 

For more information on **Sky type** and **Fog type** please refer to the visual environment page in the Scene settings section.

Once the **Sky type** and **Fog type** are chosen, you can **override their default values** by adding some a **Sky** Volume component and a **Fog** Volume component.

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