#### `protected abstract MethodInfo GetFunctionToConvert()`

## Returns

A **MethodInfo** of a class to convert to a shader function.

## Description

Defines which method within the class should be converted to a shader function. Use **Type.GetMethodInfo** to convert a method of return type **string** to a **MethodInfo** to return. The referenced class should define [Ports](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port) via [SlotAttribute](https://github.com/Unity-Technologies/ShaderGraph/wiki/CodeFunctionNode.SlotAttribute).

For more information on how to create [Nodes](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) using `CodeFunctionNode` see [Custom Nodes with CodeFunctionNode](https://github.com/Unity-Technologies/ShaderGraph/wiki/Custom-Nodes-With-CodeFunctionNode).