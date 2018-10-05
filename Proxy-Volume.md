The **Proxy Volume** is the reprojection volume used when applying a reflection.
It could be shared amongst all reflection probe's type in High Definition Render Pipeline.
For more information about reprojection and theory behind reflection, please see [Reflection and Refraction](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Reflection-and-Refraction).

### Shape
There is 3 possible shapes to use.

> **/!\\ The shape of the ProxyVolume must match the shape of the ReflectionProbe or PlanarReflectionProbe using it. Except for infinite which could match anything (see below).**

* **Box:** the reprojection volume will be box shaped and thus provide a parameter for settings its scale on three axis.
* **Sphere:** the reprojection volume will be sphere shaped and thus provide a radius parameter to tune its scale.
* **Infinite:** the reprojection is not bounded any more. This special shape provide same result than having no ProxyVolume set in affected reflection probes. It is provided only as convenience for easily changing a scene setup.

The first two shapes provide each a tool to quickly modify shape scale in the scene.
Note that the ProxyVolume is not affected by the scale of its transform. Only the position and rotation of the transform will affect its position in the scene.