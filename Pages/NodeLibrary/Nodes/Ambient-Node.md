## Description

Provides access to the Scene's **Ambient** color values. When Environment Lighting Source is set to **Gradient** [Ports](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port) **Color/Sky**, **Equator** and **Ground** return the values **Sky Color**, **Equator Color** and **Ground Color** respectively. When Environment Lighting Source is set to **Color** [Port](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port) **Color/Sky** returns the value **Ambient Color**. [Ports](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port) **Equator** and **Ground** return zero.

## Ports

| Name        | Direction           | Type  | Binding | Description |
|:------------ |:-------------|:-----|:---|:---|
| Color/Sky    | Output | Vector 3 | None | Color (Color) or Sky (Gradient) color value |
| Equator      | Output | Vector 3 | None | Equator (Gradient) color value |
| Ground       | Output | Vector 3 | None | Ground (Gradient) color value |

## Shader Code

```
float3 ColorSky = unity_AmbientSky;
float3 Equator = unity_AmbientEquator;
float3 Ground = unity_AmbientGround;
```