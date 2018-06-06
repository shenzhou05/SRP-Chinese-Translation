## Description

When using `CodeFunctionNode` you are able to define [Ports](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port) of any type available in [Shader Graph](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph). For a full list of available types see [Data Types](https://github.com/Unity-Technologies/ShaderGraph/wiki/Data-Types). Defining [Ports](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port) using `CodeFunctionNode` requires using specific types when defining a port via a method argument. 

For more information on how to create [Nodes](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) using `CodeFunctionNode` see [Custom Nodes with CodeFunctionNode](https://github.com/Unity-Technologies/ShaderGraph/wiki/Custom-Nodes-With-CodeFunctionNode).

Below is a full list including the [Data Type](https://github.com/Unity-Technologies/ShaderGraph/wiki/Data-Types) they map to.

## Port Types

| Argument Type | Data Type |
|:-------------|:------|
| Boolean | Boolean |
| Vector1 | Vector1 |
| Vector2 | Vector2 |
| Vector3 | Vector3 |
| Vector4 | Vector4 |
| Color | Vector4 (with a ColorRGBA [Port Binding](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port-Bindings)) |
| ColorRGBA | Vector4 (with a ColorRGBA [Port Binding](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port-Bindings)) |
| ColorRGB | Vector3 (with a ColorRGB [Port Binding](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port-Bindings)) |
| Texture2D | Texture2D |
| Cubemap | Cubemap |
| SamplerState | SamplerState |
| DynamicDimensionVector | DynamicVector |
| Matrix4x4 | Matrix4 |
| Matrix3x3 | Matrix3 |
| Matrix2x2 | Matrix2 |
| DynamicDimensionMatrix | DynamicMatrix |
