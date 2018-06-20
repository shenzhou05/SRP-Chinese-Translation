Operators are used to perform computation for block properties and compute custom behavior based on mathematical expressions.

##Attribute Operator

![](https://raw.githubusercontent.com/wiki/Unity-Technologies/ScriptableRenderPipeline/Pages/VFXEditor/img/attribute-operator.png)

The attribute operator is used to read a current attribute, or a source attribute. Current attribute values are those at the time of execution of the graph. Source attributes are not part of the simulation but instead part of the event that created these particles.

#### Attributes and Execution of the graph

While reading an attribute value in an operator graph, It is important to know which will be the value at a given time. 

The rule is simple : 

> Any attribute operator will fetch the attribute value at the time of execution of the block that reads it.

<u>Example 1:</u>

To illustrate this, here is an example where we set the color of particles depending on the speed of the particle.

![](https://raw.githubusercontent.com/wiki/Unity-Technologies/ScriptableRenderPipeline/Pages/VFXEditor/img/attribute-execution-1.png)

In this example, the value of the velocity attribute will be fetch during the execution of the **Set color** block. **Set velocity (Random)** will already have been executed, and the velocity values already set.

If the Set Color was placed before the Set Velocity, the value read would be the default velocity, so particles would all have the same color.

<u>Example 2:</u>

Now, what if a part of graph is used for two nodeblocks? Given our rule, the graph will be executed once for the first set color, then another time for the next set color. But the velocity will have been modified beforehand, so it will be zero the second time.

![](https://raw.githubusercontent.com/wiki/Unity-Technologies/ScriptableRenderPipeline/Pages/VFXEditor/img/execution-order-attribute.gif)

## Parameters and Inline



## Operator Library

