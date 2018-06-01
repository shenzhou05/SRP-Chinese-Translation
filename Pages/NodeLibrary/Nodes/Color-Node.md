## Description

Defines a constant **Vector 4** value in the shader using a **Color** field. Can be converted to a **Color** type [Property](https://github.com/Unity-Technologies/ShaderGraph/wiki/Property-Types) via the [Node's](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) context menu. The value of the **Mode** parameter will also be converted to the [Property](https://github.com/Unity-Technologies/ShaderGraph/wiki/Property-Types).

## Ports

| Name        | Direction           | Type  | Binding | Description |
|:------------ |:-------------|:-----|:---|:---|
| Out | Output      |    Vector 4 | None | Output value |

## Parameters

| Name        | Type           | Options  | Description |
|:------------ |:-------------|:-----|:---|
|       | Color |  | Defines the output value. |
| Mode  | Dropdown | Default, HDR | Sets properties of the Color field |