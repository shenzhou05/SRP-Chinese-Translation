## Description

A **Sub-graph** is a special type of [Shader Graph](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph). It is used to create graphs that can be referenced inside other graphs. This is useful when you wish to perform the same operations multiple times in one graph or across multiple graphs. A **Sub-graph** differs from a [Shader Graph](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph) in 3 main ways:
- [Properties](https://github.com/Unity-Technologies/ShaderGraph/wiki/Property-Types) in the [Blackboard](https://github.com/Unity-Technologies/ShaderGraph/wiki/Blackboard) of a **Sub-graph** define the input [Ports](https://github.com/Unity-Technologies/ShaderGraph/wiki/Ports) of a [Sub-graph Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Sub-graph-Node) when the **Sub-graph** is referenced in another graph.
- A **Sub-graph** has its own asset type. For more information, including how to make a new **Sub-graph**, see [Sub-graph Asset](https://github.com/Unity-Technologies/ShaderGraph/wiki/Sub-graph-Asset).
- A **Sub-graph** does not have a [Master Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Master-Node). Instead it has a [Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) called **SubGraphOutputs**. For more information see below.

For components of a **Sub-graph** see:
* [Sub-graph Asset](https://github.com/Unity-Technologies/ShaderGraph/wiki/Sub-graph-Asset)

## SubGraphOutputs

The **SubGraphOutputs** [Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) defines the output [Ports](https://github.com/Unity-Technologies/ShaderGraph/wiki/Ports) of a [Sub-graph Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Sub-graph-Node) when the **Sub-graph** is referenced in another graph. You can add and remove [Ports](https://github.com/Unity-Technologies/ShaderGraph/wiki/Ports) using the **Add Slot** and **Remove Slot** buttons.