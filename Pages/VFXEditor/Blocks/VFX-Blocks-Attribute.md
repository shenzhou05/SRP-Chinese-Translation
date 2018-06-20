Attribute blocks are used to perform generic operation over attributes.



## Set Attribute

![](https://raw.githubusercontent.com/wiki/Unity-Technologies/ScriptableRenderPipeline/Pages/VFXEditor/img/setattribute.png)

The Set Attribute block is used to set a value directly to an attribute with options.

* **Composition** : Overwrite, Add, Scale or Blend 
* **Random** : Off (Constant), Uniform or Per-Component
* **Source** : Slot (Value taken from the Input Property) or Source Attribute
* **Channels** : When setting values to a variadic attribute, you can specify channels.

Setting source to Source Attribute transforms the Set Attribute node to **Inherit Source Attribute** where the value is not fetched from the Input property but from the **Source Attribute** instead.

## Attribute from Curve



## Attribute from Map

