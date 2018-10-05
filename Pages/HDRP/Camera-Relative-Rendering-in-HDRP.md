# Camera-Relative Rendering in HDRP

## What is it?

The purpose of camera-relative rendering is to make rendering of distant objects (with large world space coordinates) more robust and numerically stable.

## How does it work?

It accomplishes the task by translating objects and lights by the negated world space camera position (into the so-called camera-relative world space) prior to performing any other geometric transformations. The world space camera position is then subsequently set to 0, and all relevant matrices are modified accordingly.

Therefore, in the shader, expect view and view-projection matrices (and their inverses) to be camera-relative, along with light (e.g. LightData.positionWS) and surface (e.g. PositionInputs.positionWS) positions. Expect most world space positions you encounter in HDRP shaders to be camera-relative. Note that _WorldSpaceCameraPos is never camera-relative, as it’s used for coordinate space conversion.

## How can I enable it?

It is enabled by default in ShaderConfig.cs. If you change the value in the file, make sure to Generate Shader Includes in order to update ShaderConfig.cs.hlsl.

## How do I switch between coordinate spaces?

Use GetAbsolutePositionWS() and GetCameraRelativePositionWS() defined in ShaderVariablesFunctions.hlsl.

## Examples

### If camera-relative rendering is enabled:

GetAbsolutePositionWS(PositionInputs.positionWS) returns the non-camera-relative world space position.

GetAbsolutePositionWS(float3(0, 0, 0)) returns the world space position of the camera equal to _WorldSpaceCameraPos.

GetCameraRelativePositionWS(_WorldSpaceCameraPos) returns float3(0, 0, 0).

### If camera-relative rendering is disabled:

GetAbsolutePositionWS() and GetCameraRelativePositionWS() return the position passed to the function without any modification.