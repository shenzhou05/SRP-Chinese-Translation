## Description

Defines a constant **Texture 2D Asset** for use in the shader. To sample the **Texture 2D Asset** it should be used in conjunction with a [Sample Texture 2D Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Sample-Texture-2D-Node). When using a separate **Texture 2D Asset Node** you can sample a **Texture 2D** twice, with different parameters, without defining the **Texture 2D** itself twice.

## Ports

| Name        | Direction           | Type  | Binding | Description |
|:------------ |:-------------|:-----|:---|:---|
| Out | Output      |    Texture | None | Output value |

## Parameters

| Name        | Type           | Options  | Description |
|:------------ |:-------------|:-----|:---|
|       | Object Field (Texture) | | Defines the texture asset from the project. |