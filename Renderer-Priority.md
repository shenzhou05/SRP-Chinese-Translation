Renderer Priority is used as an additional sorting parameter for Renderers.

In Unity, objects can be sorted in many ways during rendering but one of the most important is sorting by Render Queue. Render Queue is a material property so it means that it can be used to sort a group objects using different materials but not objects using the same material.
Renderer Priority, as a per Renderer property allows user to achieve that. Many objects using the same material can be sorted by changing their Renderer Priority. Objects will be sorted by Render Queue first, then Renderer Priority.

Renderer Priority can be changed in several ways:

- Via script with Renderer objects renderPriority property (https://docs.unity3d.com/2018.3/Documentation/ScriptReference/Renderer-rendererPriority.html)
- In various Renderers UI as Transparency Priority in HDRP

You will notice that it has two different names. As this parameter is cross Render Pipeline and can be used in many different ways depending on the pipeline, the name of the scripting property is pipeline agnostic. In HDRP though, it's only used to sort transparent objects so it was exposed as such in the HDRP various Renderers UI.