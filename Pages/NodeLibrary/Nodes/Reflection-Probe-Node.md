## Description

Provides access to the nearest **Reflection Probe** to the object. Requires **Normal** and **View Direction** to sample the probe. You can supply a blurring effect by sampling at a different Level of Detail using the **LOD** input.

## Ports

| Name        | Direction           | Type  | Binding | Description |
|:------------ |:-------------|:-----|:---|:---|
| View Dir      | Input | Vector 3 | View Direction (object space) | Mesh's view direction |
| Normal | Input      |    Vector 3 | Normal (object space) | Mesh's normal vector |
| LOD | Input      |    Vector 1 | None | Level of detail for sampling |
| Out | Output      |    Vector 3 | None | Output color value |

## Shader Function

```
float3 reflectVec = reflect(-ViewDir, Normal);
Out = DecodeHDREnvironment(SAMPLE_TEXTURECUBE_LOD(unity_SpecCube0, samplerunity_SpecCube0, reflectVec, LOD), unity_SpecCube0_HDR);
```