#### `Attribute in CodeFunctionNode`

## Description

Defines an argument to a method as a [Port](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port) for a [Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node). The type of the [Port](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port) is defined by the argument type.

The **SlotAttribute** can also be used to apply a [Port Binding](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port-Bording) to the [Port](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port) or define its default value.

## Properties

| Property    | Type | Description |
|:------------|:-----|:------------|
| slotId | int | Index for the [Port](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port). Must be unique. |
| binding | [Binding](https://github.com/Unity-Technologies/ShaderGraph/wiki/CodeFunctionNode.Binding) | Defines the [Port Binding](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port-Bording). Set to **None** for no binding. |
| hidden | bool | If true the [Port](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port) will be hidden. |
| defaultValue | Vector4 | Default value for the [Port](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port). |