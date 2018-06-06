## Description

Defines a constant **Cubemap Asset** for use in the shader. To sample the **Cubemap Asset** it should be used in conjunction with a [Sample Cubemap Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Sample-Cubemap-Node). When using a separate **Cubemap Asset Node** you can sample a **Cubemap** twice, with different parameters, without defining the **Cubemap** itself twice.

## Ports

| Name        | Direction           | Type  | Binding | Description |
|:------------ |:-------------|:-----|:---|:---|
| Out | Output      |    Cubemap | None | Output value |

## Parameters

| Name        | Type           | Options  | Description |
|:------------ |:-------------|:-----|:---|
|       | Object Field (Cubemap) | | Defines the cubemap asset from the project. |