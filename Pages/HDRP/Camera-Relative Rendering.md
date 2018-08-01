__Camera-Relative Rendering in the HDRP__

__What is it?__

The purpose of camera-relative rendering is to make rendering of distant objects (with large world space coordinates) more robust and numerically stable.

__How does it work?__

It accomplishes the task by translating objects and lights by the negated world space camera position (into the so-called camera-relative world space) prior to performing any other geometric transformations. The world space camera position is then subsequently set to 0, and all relevant matrices are modified accordingly.

Therefore, in the shader, expect view and view-projection matrices (and their inverses) to be camera-relative, along with light (e.g. *LightData.positionWS*) and surface (e.g. *PositionInputs.positionWS*) positions. Expect most world space positions you encounter in HDRP shaders to be camera-relative. Note that *_WorldSpaceCameraPos* is never camera-relative, as it’s used for coordinate space conversion.

__How can I enable it?__

It is enabled by default in *ShaderConfig.cs*. If you change the value in the file, make sure to *Generate Shader Includes* in order to update *ShaderConfig.cs.hlsl*.

__How do I switch between coordinate spaces?__

Use *GetAbsolutePositionWS()* and *GetCameraRelativePositionWS()* defined in *ShaderVariablesFunctions.hlsl*.

__Examples__

If camera-relative rendering is __enabled__:

*GetAbsolutePositionWS(PositionInputs.positionWS) *returns the non-camera-relative world space position.

*GetAbsolutePositionWS(float3(0, 0, 0))* returns the world space position of the camera equal to *_WorldSpaceCameraPos.*

*GetCameraRelativePositionWS(_WorldSpaceCameraPos) *returns* float3(0, 0, 0)*.

If camera-relative rendering is __disabled__:

*GetAbsolutePositionWS() and GetCameraRelativePositionWS() *return the position passed to the function without any modification.
