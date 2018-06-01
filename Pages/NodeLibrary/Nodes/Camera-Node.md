## Description

Provides access to various parameters of the current **Camera**. This is comprised of parameters of the **Camera** GameObject, such as Position and Direction, as well as various projection parameters.

## Ports

| Name        | Direction           | Type  | Binding | Description |
|:------------ |:-------------|:-----|:---|:---|
| Position      | Output | Vector 3 | None | Position of the Camera's GameObject to world space |
| Direction       | Output | Vector 3 | None | The Camera's forward vector direction |
| Orthographic    | Output | Vector 1 | None | Returns 1 if the Camera is orthographic, otherwise 0 |
| Near Plane       | Output | Vector 1 | None | The Camera's near plane distance |
| Far Plane       | Output | Vector 1 | None | The Camera's far plane distance |
| Z Buffer Sign   | Output | Vector 1 | None | Returns -1 when using a reversed Z Buffer, otherwise 1 |
| Width       | Output | Vector 1 | None | The Camera's width if orthographic |
| Height       | Output | Vector 1 | None | The Camera's height if orthographic |

## Shader Code

```
float3 Position = _WorldSpaceCameraPos;
float3 Direction = -1 * mul(unity_ObjectToWorld, UNITY_MATRIX_IT_MV [2].xyz);
float Orthographic = unity_OrthoParams.w;
float NearPlane = _ProjectionParams.y;
float FarPlane = _ProjectionParams.z;
float ZBufferSign = _ProjectionParams.x;
float Width = unity_OrthoParams.x;
float Height = unity_OrthoParams.y;
```