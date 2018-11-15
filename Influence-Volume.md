The **Influence Volume** is the area impacted by the reflection probe. 
For more information about theory behind reflection, please see [Reflection and Refraction](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Reflection-and-Refraction).

## Shape
There is 2 possible shape to use.

> **/!\\ The shape of the Influence Volume must match the shape of the [ProxyVolume](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Proxy-Volume) if one is used.**

* **Box:** the influenced area will be box shaped and thus provide a parameter for settings its scale on three axis.
* **Sphere:** the influenced area will be sphere shaped and thus provide a radius parameter to tune its scale.

## Offset
### Reflection Probe
The Capture point is the center of the **ReflectionProbe**. The offset parameter allows to decal the InfluenceVolume from that capture point.
### Planar Reflection Probe
The capture point is computed regarding the camera currently rendering.

## Blends
There is three blend values that can change how the way objects in the influence volume are impacted.

Each of this blends could be simply manipulated with a scalar value in _Normal_ mode. For a more precise settings with a box shape, the _Advanced_ mode allow to modify distance from each face of the box.
### Blend distance
This is used to define a distance between the exterior of the influence volume and the area where the reflection fully impact object. Anything in this range will only receive a portion or the reflection. In above picture, the **InfluenceVolume** shape is in yellow and the distance is in Green. Portion of the plane in between is affected progressively.