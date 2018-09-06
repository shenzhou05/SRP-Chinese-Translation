# Environment lighting

What we refer to as environment lighting is the lighting produced by the environment surrounding our unity scene. Most commonly this represents the sky lighting, but it can also represent a different kind of background (light a lighting studio, or any kind of background).

In HD render pipeline, environment lighting is setup through **Volumes** and **volume profiles**.

The **Environment lighting** section in the Light settings window is replaced in HD render pipeline by this setup per Volume so that you can smoothly interpolate between different sets of settings for your sky and fog per game area.

The two key concepts for environment lighting are the **visual environment**, and the **baking environment**.

## Visual environment

**Visual environment** is a Volume component that informs the render pipeline about what type of sky and fog you want to see through your game camera. 

For more information on **Sky type** and **Fog type** please refer to the visual environment page in the Scene settings section.

Once the **Sky type** and **Fog type** are chosen, you can **override their default values** by adding some a **Sky** Volume component and a **Fog** Volume component.

## Baking environment

Baking environment is a component called "**Baking sky**" that informs the Unity Editor which sky to use for **light baking**.

This component references a **Volume profile** that just needs to include some sky settings. These sky settings will directly drive the sky used for light baking.

This volume profile can be a profile assigned to a Volume in your scene (so it matches the sky that is visible at runtime ) or it can be a different one if you want to control your light baking separately.

**A typical use case** for using a different profile for the Baking Sky is a HDRI sky that includes the sunlight: You probably want to have a sunlight visible when you play your game, but you could want to use a different HDRI sky where the sun is erased for light baking because you have a directional light in your scene that contributes to the lighting as the Sunlight (and thus baking lighting with a HDRI that includes the sun would make the sun contribute to the lighting twice).

## Reflections

Note on reflections :

Baked reflection probes will render using the baking environment, as this is consistent with your baking settings.

Realtime reflection probes will render using the visual environment, as this is consistent with what you'll see with your game camera at runtime.

## Adding your own Sky Type

Please refer to the Advanced section for instructions on how to add your own Sky Type to HD render pipeline.