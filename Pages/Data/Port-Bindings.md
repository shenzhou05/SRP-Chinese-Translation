## Description

Some input [Ports](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port) might have **Port Bindings**. This means there is an expectation of the data that should be supplied to the [Port](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port), such as a **Normal Vector** or **UV**. However, a **Port Binding** only affects a [Port](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port) that does not have a connected [Edge](https://github.com/Unity-Technologies/ShaderGraph/wiki/Edge). These [Ports](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port) still have a regular [Data Type](https://github.com/Unity-Technologies/ShaderGraph/wiki/Data-Types) that define what [Edges](https://github.com/Unity-Technologies/ShaderGraph/wiki/Edge) can be connected to them.

In practice this means that if no [Edge](https://github.com/Unity-Technologies/ShaderGraph/wiki/Edge) is connected to the [Port](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port) the default data used in that port will be taken from its **Port Binding**. A full list of **Port Bindings** and their associated default options is found below.

## Port Bindings List

| Name        | Data Type | Options           | Description |
|:------------|:----------|:------------------|:------------|
| Bitangent | Vector 3 |  | Vertex or fragment bitangent, label describes expected transform space |
| Color | Vector 4 |  |RGBA Color picker |
| ColorRGB | Vector 3 |  | RGB Color picker |
| Normal | Vector 3 |  | Vertex or fragment normal vector, label describes expected transform space |
| Position | Vector 3 |  | Vertex or fragment position, label describes expected transform space |
| Normal | Vector 3 |  | Vertex or fragment normal vector, label describes expected transform space |
| Screen Position | Vector 4 |  | Default, Raw, Center, Tiled | Vertex or fragment position in screen space. Dropdown selects mode. See [Screen Position Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Screen-Position-Node) for details |
| Tangent | Vector 3 |  | Vertex or fragment tangent vector, label describes expected transform space |
| UV | Vector 2 |  | UV0, UV1, UV2, UV3 | Mesh UV coordinates. Dropdown selects UV channel. |
| Vertex Color | Vector 4 |  | RGBA vertex color value. |
| View Direction | Vector 3 |  | Vertex or fragment view direction vector, label describes expected transform space |