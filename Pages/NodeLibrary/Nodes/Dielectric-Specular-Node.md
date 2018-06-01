## Description

Returns a **Dielectric Specular** F0 value for a physically based material. The material to use can be selected with the **Material** dropdown parameter on the [Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node).

A **Common** **Material** type defines a range between 0.024 and 0.048 sRGB values. The value between this range can be selected with the **Range** parameter. This **Material** type should be used for various materials such as plastics and fabrics.

You can use **Custom** material type to define your own physically based material value. The output value in this case is defined by its index of refraction. This can be set by the parameter **IOR**.

## Ports

| Name        | Direction           | Type  | Binding | Description |
|:------------ |:-------------|:-----|:---|:---|
| Out | Output      |    Vector 3 | None | Output value |

## Parameters

| Name        | Type           | Options  | Description |
|:------------ |:-------------|:-----|:---|
| Material | Dropdown | Common, RustedMetal, Water, Ice, Glass, Custom | Selects the material value to output. |
| Range    | Slider |  | Controls output value for **Common** material type. |
| IOR      | Slider |  | Controls index of refraction for **Custom** material type. |

## Shader Function

**Common**
```
float3 Out = lerp(0.034, 0.048, _Node_Range);
```

**RustedMetal**
```
float3 Out = float3(0.030, 0.030, 0.030);
```

**Water**
```
float3 Out = float3(0.020, 0.020, 0.020);
```

**Ice**
```
float3 Out = float3(0.018, 0.018, 0.018);
```

**Glass**
```
float3 Out = float3(0.040, 0.040, 0.040);
```

**Custom**
```
float3 Out = pow(_Node_IOR - 1, 2) / pow(_Node_IOR + 1, 2);
```