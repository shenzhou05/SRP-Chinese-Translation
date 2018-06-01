## Description

An **Edge** defines a connection between two [Ports](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port). **Edges** define how data flows through the [Shader Graph](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph) node network. They can only be connected from an input [Port](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port) to an output [Port](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port).

Each **Edge** has a [Data Type](https://github.com/Unity-Technologies/ShaderGraph/wiki/Data-Types) which defines what [Ports](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port) it can be connected to. Each [Data Type](https://github.com/Unity-Technologies/ShaderGraph/wiki/Data-Types) has an associated color for identifying its type.

You can create a new **Edge** by dragging from a [Port](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port) with left mouse button. Edges can be deleted with Delete (Windows) or Command + Backspace (OSX).

You can open a contextual [Create Node Menu](https://github.com/Unity-Technologies/ShaderGraph/wiki/Create-Node-Menu) by dragging an **Edge** from a [Port](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port) with left mouse button and releasing it in an empty area of the workspace.