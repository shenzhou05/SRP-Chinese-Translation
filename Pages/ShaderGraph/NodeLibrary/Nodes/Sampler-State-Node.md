## Description

Defines a **Sampler State** for sampling textures. It should be used in conjunction with sampling [Nodes](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) such as the [Sample Texture 2D Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Sample-Texture-2D-Node). You can set a filter mode with the dropdown parameter **Filter** and a wrap mode with the dropdown parameter **Wrap**.

When using a separate **Sample State Node** you can sample a **Texture 2D** twice, with different sampler parameters, without defining the **Texture 2D** itself twice.

Some filtering and wrap modes are only available on certain platforms.

## Ports

| Name        | Direction           | Type  | Binding | Description |
|:------------ |:-------------|:-----|:---|:---|
| Out | Output      | Sampler State | None | Output value |

## Parameters

| Name        | Type           | Options  | Description |
|:------------ |:-------------|:-----|:---|
| Filter | Dropdown | Linear, Point, Trilinear | Defines filtering mode for sampling. |
| Wrap   | Dropdown | Repeat, Clamp, Mirror, MirrorOnce | Defines wrap mode for sampling. |