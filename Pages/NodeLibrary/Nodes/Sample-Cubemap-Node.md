## Description

Samples a **Cubemap** and returns a **Vector 4** color value for use in the shader. Requires **View Direction** and **Normal** inputs to sample the **Cubemap**. You can supply a blurring effect by sampling at a different Level of Detail using the **LOD** input.

## Ports

| Name        | Direction           | Type  | Binding | Description |
|:------------ |:-------------|:-----|:---|:---|
| Cube | Input      |    Cubemap | None | Cubemap to sample |
| View Dir      | Input | Vector 3 | View Direction (object space) | Mesh's view direction |
| Normal | Input      |    Vector 3 | Normal (object space) | Mesh's normal vector |
| LOD | Input      |    Vector 1 | None | Level of detail for sampling |
| Out | Output      | Vector 4 | None | Output value |