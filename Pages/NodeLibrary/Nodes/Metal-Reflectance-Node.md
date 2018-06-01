## Description

Returns a **Metal Reflectance** value for a physically based material. The material to use can be selected with the **Material** dropdown parameter on the [Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node).

When using **Specular** **Workflow** on a [PBR Master Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/PBR-Master-Node) this value should be supplied to the **Specular** [Port](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port). When using **Metallic** **Workflow** this value should be supplied to the **Albedo** [Port](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port). 

## Ports

| Name        | Direction           | Type  | Binding | Description |
|:------------ |:-------------|:-----|:---|:---|
| Out | Output      |    Vector 3 | None | Output value |

## Parameters

| Name        | Type           | Options  | Description |
|:------------ |:-------------|:-----|:---|
| Material | Dropdown | Iron, Silver, Aluminium, Gold, Copper, Chromium, Nickel, Titanium, Cobalt, Platform | Selects the material value to output. |

## Shader Function

**Iron**
```
float3 Out = float3(0.560, 0.570, 0.580);
```

**Silver**
```
float3 Out = float3(0.972, 0.960, 0.915);
```

**Aluminium**
```
float3 Out = float3(0.913, 0.921, 0.925);
```

**Gold**
```
float3 Out = float3(1.000, 0.766, 0.336);
```

**Copper**
```
float3 Out = float3(0.955, 0.637, 0.538);
```

**Chromium**
```
float3 Out = float3(0.550, 0.556, 0.554);
```

**Nickel**
```
float3 Out = float3(0.660, 0.609, 0.526);
```

**Titanium**
```
float3 Out = float3(0.542, 0.497, 0.449);
```

**Cobalt**
```
float3 Out = float3(0.662, 0.655, 0.634);
```

**Platinum**
```
float3 Out = float3(0.672, 0.637, 0.585);
```