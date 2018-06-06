## Description

Defines a **Vector 4** value in the shader. If [Ports](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port) **X**, **Y**, **Z** and **W** are not connected with [Edges](https://github.com/Unity-Technologies/ShaderGraph/wiki/Edge) this [Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) defines a constant **Vector 4**, otherwise this [Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) can be used to combine various **Vector 1** values.

## Ports

| Name        | Direction           | Type  | Binding | Description |
|:------------ |:-------------|:-----|:---|:---|
| X      | Input | Vector 1 | None | Input x component value |
| Y      | Input | Vector 1 | None | Input y component value |
| Z      | Input | Vector 1 | None | Input z component value |
| W      | Input | Vector 1 | None | Input w component value |
| Out | Output      |    Vector 4 | None | Output value |

## Shader Code

```
float4 Out = float4(X, Y, Z, W);
```