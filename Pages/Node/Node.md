## Description

A **Node** defines an input, output or operation on the [Shader Graph](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph), depending on its available [Ports](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port). A **Node** may have any number of input and/or output [Ports](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port). You create a [Shader Graph](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph) by connecting these [Ports](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port) with [Edges](https://github.com/Unity-Technologies/ShaderGraph/wiki/Edge). A **Node** might also have any number of **Parameters**, these are controls on the **Node** that do not have [Ports](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port).

You can collapse a **Node** by clicking the **Collapse** button in the top-right corner of the **Node**. This will hide all unconnected [Ports](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port).

For components of a **Node** see:
* [Port](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port)
* [Edge](https://github.com/Unity-Technologies/ShaderGraph/wiki/Edge)

There are many available **Nodes** in [Shader Graph](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph). For a full list of all available **Nodes** see the [Node Library](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node-Library).

## Preview

Some **Nodes** have a preview on the **Node**. This preview displays the main output value at that stage in the graph. The preview can be hidden with the **Collapse** button at the top of the preview. This is displayed when the mouse cursor is hovering over the node. You can also collapse and expand previews on all node via the context menu on the [Shader Graph Window](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph-Window).

## Context Menu

Right clicking on a **Node** will open a context menu. This menu contains many operations that can be performed on the **Node**. Note that when multiple nodes are selected, these operations will be applied to the entire selection.

| Item        | Description |
|:------------|:------------|
| Copy Shader | Copies the generated HLSL code at this stage in the graph to the clipboard |
| Disconnect All | Removes all [Edges](https://github.com/Unity-Technologies/ShaderGraph/wiki/Edge) from all [Ports](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port) on the **Node(s)** |
| Cut | Cuts selected **Node(s)** to the clipboard |
| Copy | Copies selected **Nodes(s)** to the clipboard |
| Paste | Pastes **Node(s)** in the clipboard |
| Delete | Deletes selected **Node(s)** |
| Duplicate | Duplicates selected **Node(s)** |
| Convert To Sub-graph | Creates a new [Sub-graph Asset](https://github.com/Unity-Technologies/ShaderGraph/wiki/Sub-graph-Asset) with the selected **Node(s)** included |
| Convert To Inline Node | Converts a [Property Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Property-Node) into a regular node of the appropriate [Data Type](https://github.com/Unity-Technologies/ShaderGraph/wiki/Data-Types) |
| Convert To Property | Converts a **Node** into a new **Property** on the [Blackboard](https://github.com/Unity-Technologies/ShaderGraph/wiki/Blackboard) of the appropriate [Property Type](https://github.com/Unity-Technologies/ShaderGraph/wiki/Property-Types) |
| Open Documentation | Opens a new web browser to the selected **Nodes** documentation page in the [Node Library](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node-Library) |