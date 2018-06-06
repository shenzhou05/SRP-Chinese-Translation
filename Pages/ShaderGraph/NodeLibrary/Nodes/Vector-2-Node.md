## Description

Defines a **Vector 2** value in the shader. If [Ports](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port) **X** and **Y** are not connected with [Edges](https://github.com/Unity-Technologies/ShaderGraph/wiki/Edge) this [Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) defines a constant **Vector 2**, otherwise this [Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) can be used to combine various **Vector 1** values.

## Ports

| Name        | Direction           | Type  | Binding | Description |
|:------------ |:-------------|:-----|:---|:---|
| X      | Input | Vector 1 | None | Input x component value |
| Y      | Input | Vector 1 | None | Input y component value |
| Out | Output      |    Vector 2 | None | Output value |

## Shader Code

```
float2 Out = float2(X, Y);
```