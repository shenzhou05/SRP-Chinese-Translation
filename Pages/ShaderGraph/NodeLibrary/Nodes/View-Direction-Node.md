## Description

Provides access to the mesh vertex or fragment's **View Direction** vector. This is the vector from the vertex or fragment to the camera. The coordinate space of the output value can be selected with the **Space** dropdown parameter.

## Ports

| Name        | Direction           | Type  | Binding | Description |
|:------------ |:-------------|:-----|:---|:---|
| Out | Output      |    Vector 3 | None | Mesh's **View Direction** vector. |

## Parameters

| Name        | Type           | Options  | Description |
|:------------ |:-------------|:-----|:---|
| Space | Dropdown | Object, View, World, Tangent | Selects coordinate space of **View Direction** to output. |