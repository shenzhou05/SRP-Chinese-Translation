## Description

Provides access to the **Light Probe** parameters at the object's position. Requires **Normal** input for probe sampling.

## Ports

| Name        | Direction           | Type  | Binding | Description |
|:------------ |:-------------|:-----|:---|:---|
| Normal      | Input | Vector 3 | Normal (world space) | Mesh **Normal** data |
| Out       | Output | Vector 3 | None | Output color value |

## Shader Function

```
Out = SampleSH(Normal);
```