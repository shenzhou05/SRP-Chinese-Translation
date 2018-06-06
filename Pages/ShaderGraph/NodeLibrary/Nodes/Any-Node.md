## Description

Returns true if any of the components of the input **In** are non-zero. This is useful for [Branching](https://github.com/Unity-Technologies/ShaderGraph/wiki/Branch-Node).

## Ports

| Name        | Direction           | Type  | Binding | Description |
|:------------ |:-------------|:-----|:---|:---|
| In      | Input | Dynamic Vector | None | Input value |
| Out | Output      |    Boolean | None | Output value |

## Shader Function

`Out = any(In)`