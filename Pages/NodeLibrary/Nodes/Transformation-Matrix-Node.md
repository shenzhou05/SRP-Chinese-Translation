## Description

Defines a constant **Matrix 4x4** value for a default Unity **Transformation Matrix** in the shader. The **Transformation Matrix** can be selected from the dropdown parameter.

## Ports

| Name        | Direction           | Type  | Binding | Description |
|:------------ |:-------------|:-----|:---|:---|
| Out | Output      |    Matrix 4 | None | Output value |

## Parameters

| Name        | Type           | Options  | Description |
|:------------ |:-------------|:-----|:---|
|  | Dropdown | ModelView, View, Projection, ViewProjection, TransposeModelView, InverseTransposeModelView, ObjectToWorld, WorldToObject | Sets output value |

## Shader Code

**ModelView**
```
float4x4 Out = UNITY_MATRIX_MV;
```

**View**
```
float4x4 Out = UNITY_MATRIX_V;
```

**Projection**
```
float4x4 Out = UNITY_MATRIX_P;
```

**ViewProjection**
```
float4x4 Out = UNITY_MATRIX_VP;
```

**TransposeModelView**
```
float4x4 Out = UNITY_MATRIX_T_MV;
```

**InverseTransposeModelView**
```
float4x4 Out = UNITY_MATRIX_IT_MV;
```

**ObjectToWorld**
```
float4x4 Out = UNITY_MATRIX_M;
```

**WorldToObject**
```
float4x4 Out = UNITY_MATRIX_I_M;
```