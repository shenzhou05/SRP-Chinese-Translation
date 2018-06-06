## Description

Defines a **Vector 3** value in the shader. If [Ports](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port) **X**, **Y** and **Z** are not connected with [Edges](https://github.com/Unity-Technologies/ShaderGraph/wiki/Edge) this [Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) defines a constant **Vector 3**, otherwise this [Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) can be used to combine various **Vector 1** values.

## Ports

| Name        | Direction           | Type  | Binding | Description |
|:------------ |:-------------|:-----|:---|:---|
| X      | Input | Vector 1 | None | Input x component value |
| Y      | Input | Vector 1 | None | Input y component value |
| Z      | Input | Vector 1 | None | Input z component value |
| Out | Output      |    Vector 3 | None | Output value |

## Shader Code

```
float3 Out = float3(X, Y, Z);
```