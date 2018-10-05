How motion vector work in builtin Unity?
- If you have a motion vector pass AND you have( a) transform matrix change, b) force no motion, c) skinning/blendshape), then you render object motion vector.
- If you have motion vector pass AND you don't respect condition above you render nothing
- if you don't have motion vector pass there is no object motion vector
- All shader have a motion vector pass (or have a fallback if not declare)

With builtin unity, you can't have wind vertex animation on an object if it doesn't move.
For SRP we wanted to change this behavior, so we have update thing as we can and still be compatible with builtin Unity.

How motion vector work in SRP Unity?
- If you have a motion vector pass enabled then you render object motion vector.
- If you have a motion vector pass disabled AND you have( a) transform matrix change, b) force no motion, c) skinning/blendshape), then you render object motion vector.
- if you don't have motion vector pass there is no object motion vector
- Any custom shader need to add a "MotionVector" pass - It need to be *disabled by default* and enabled if there is a need for vertex or texture animated motion vector

Currently Lit shader handle the last point in BaseUnlitUI.cs and this is manage by the inspector.

**Guidelines when writing a material**

In HDRP there is an optimization that don't render an object in the depth prepass if it render object motion vector. In this case, the motion vector pass is done just after the depth prepass and complete the depth buffer in addition to filling the motion vector buffer. This save some drawcall.
However to work with such a framework the material need to follow some guidelines.

As explain above every material in HDRP must have a MotionVector pass.
(Note: Thing like terrain shouldn't be require to have MotionVector pass, currently (4.0.0) there is one but this will be remove in the future unity release).

Shader need to declare _EnableMotionVectorForVertexAnimation property, this is recognize in BaseUnlitUI.cs to disable the MotionVector pass per default.