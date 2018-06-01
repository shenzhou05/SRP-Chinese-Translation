## Description

Provides access to various **Time** parameters in the shader.

## Ports

| Name        | Direction           | Type  | Binding | Description |
|:------------ |:-------------|:-----|:---|:---|
| Time | Output      |    Vector 1 | None | Time value |
| Sine Time | Output      |    Vector 1 | None | Sine of Time value |
| Cosine Time | Output      |    Vector 1 | None | Cosine of Time value |
| Delta Time | Output      |    Vector 1 | None | Current frame time |
| Smooth Delta | Output      |    Vector 1 | None | Current frame time smoothed |

## Shader Code

```
float Time = _Time.y;
float SineTime = _SinTime.w;
float CosineTime = _CosTime.w;
float DeltaTime = unity_DeltaTime.x;
float SmoothDelta = unity_DeltaTime.z;
```