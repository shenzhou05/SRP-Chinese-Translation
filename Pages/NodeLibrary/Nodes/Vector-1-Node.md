## Description

Defines a **Vector 1** value in the shader. If [Port](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port) **X** is not connected with an [Edge](https://github.com/Unity-Technologies/ShaderGraph/wiki/Edge) this [Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) defines a constant **Vector 1**.

## Ports

| Name        | Direction           | Type  | Binding | Description |
|:------------ |:-------------|:-----|:---|:---|
| X      | Input | Vector 1 | None | Input x component value |
| Out | Output      |    Vector 1 | None | Output value |

## Shader Code

```
float Out = X;
```