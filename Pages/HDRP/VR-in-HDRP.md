# VR Support in HDRP
This page describes how to set up your HDRP project for VR and calls out currently unsupported features. 

## Configure HDRP for VR
Most of the following settings can be configured in the [HDRenderPipeline Asset](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/HDRP-Asset). 
Some settings may need to be set up under Default Frame Settings, in addition to where they would be set under Render Pipeline Settings or Player Settings. 

**Required:**
* Camera relative rendering off
* Support only forward rendering
* Enable VR under Player Settings
* Enable FPTL for forward off

**Recommended:**
* Enable MSAA

In order to turn off camera-relative rendering, modify ShaderConfig.cs and ShaderConfig.cs.hlsl to change CameraRelativeRendering and SHADEROPTIONS_CAMERA_RELATIVE_RENDERING from 1 to 0.

To support only forward rendering, Forward must be selected in the Lit shader mode drop-down in both Rendering Settings and Default Frame Settings. 

MSAA is the recommended anti-aliasing solution for VR because it is hardware-accelerated and anti-aliases scenes without blurring away too much detail. However, in scenes with many high-frequency details (like leaves or grass), the aggressive smoothing from PostProcessing's TAA may be preferred despite the hit to performance. 

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

## Troubleshooting
**Game view shows unexpected or indecipherable view of scene**
Deselect the Main Camera in your scene. 