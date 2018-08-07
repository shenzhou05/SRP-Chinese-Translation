This frequently asked question document (FAQ) aim at answering regular question about HDRPUser questions

## Is AR/VR supported?

No.

## Is Unity Terrain supported?

No. Upcoming Terrain update should fix this issue.

## Is Shuriken supported?

Only unlit particles of Shuriken are supported, Lit particles aren’t. This is because HDRP use an entirely new lighting system not compatible with Shuriken. There is a new VFX graph in development that will solve this issue.

## Why is my Skybox material not doing anything?

Sky and fog are handled differently in HDRP so the lighting panel skybox settings should not be used ([https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/sky-and-fog](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/sky-and-fog))

## How to do water?

Use planar reflection component and a rough refraction transparent material.

## How to add volumetric fog?

Sky and fog are handled differently in HDRP so the lighting panel skybox settings should not be used. Use volume settings to add a volumetric fog component and select volumetric fog on visual environment. More information: ([https://docs.google.com/document/d/1bH4UIEr-t1B18Tu5ZjVobtSei2f-epSJACoUMOc7M64](https://docs.google.com/document/d/1bH4UIEr-t1B18Tu5ZjVobtSei2f-epSJACoUMOc7M64))

## How to do planar reflections?

Add a planar reflection component. The plan will be oriented based on the attached entity.

See documentation for more information.

## How to change the resolution of planar reflections?

Planar reflection resolution is control on the render pipeline asset.

## Are Culling Mask on light working like in Builtin ?

Not supported. No alternative currently.

# Development questions

## Why RenderTarget of GBuffer aren’t cleared?

This is an optimization. Clearing a RenderTarget have a cost and the GBuffer don’t need to be clear as at everywhere the whole GBuffer is overwrite. It is however possible that part of the GBuffer is not overwrite, this happen when the stencil buffer is tagged with StencilLightingUsage.NoLighting (For the mask StencilBitMask.LightingMask) for forward material or sky for example. In this case, this part of the GBuffer shouldn’t be read or processed as it doesn’t include any relevant information.

## How FrameSettings work?

There is DefaultFrameSettings (Inspector of Render Pipeline Asset) for the scene view in editor and for camera that use Default render path

There is SerializedFrameSettings for each camera that are use to init the value of a camera (Edit with the inspector of HD Camera when the RenderPath is set to custom)

There is FrameSettings for each camera that store the current value to use (These one under the influence of the debug windows)

At init of player, we init FrameSettings to serializedFrameSettings or DefaultFrameSettings (edited)

Then debug windows can modify them.

Individually for each camera, for debug purpose

## How to reference shader include file from the package?

To reference shader files from your project you can use these path:

#include "CoreRP/ShaderLibrary/Common.hlsl"

#include "HDRP/ShaderPass/ShaderPassVelocity.hlsl"

The CoreRP and HDRP root for shader compilation are configure by the Core and HDShaderIncludePaths.cs
