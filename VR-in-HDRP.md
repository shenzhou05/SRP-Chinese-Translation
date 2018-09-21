# VR Support in HDRP
This page describes how to set up your HDRP project for VR, calls out currently-unsupported features, and shows how to write and add shaders that will work when rendering in stereo. 

## Configure HDRP for VR
Most of the following settings can be configured in the [HDRenderPipeline Asset](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/HDRP-Asset). 
Some settings may need to be set up under Default Frame Settings, in addition to where they would be set under Render Pipeline Settings or Player Settings. 

**Required:**
* Camera relative rendering off
* Support only forward rendering
* Enable Stereo under FrameSettings
* Enable VR under Player Settings

**Recommended:**
* Enable MSAA

In order to turn off camera-relative rendering, modify ShaderConfig.cs and ShaderConfig.cs.hlsl to change CameraRelativeRendering and SHADEROPTIONS_CAMERA_RELATIVE_RENDERING from 1 to 0.

MSAA is the go-to anti-aliasing solution for VR, since it is hardware accelerated and thus minimizes performance impact. If performance is not an issue, TAA may be enabled in PostProcessing instead.

## Currently Unsupported
The following features are not currently supported in HDRP for VR.

**HDRP Features:**
* Deferred lighting
* Compute light evaluation
* Reflections (SSR)
* Debug display
* Decals
* Distortion

**VR Features:**
* Viewport scale
* Render scale
* Occlusion mesh ([PR in progress](https://github.com/Unity-Technologies/ScriptableRenderPipeline/pull/1943))