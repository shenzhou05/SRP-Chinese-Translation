## Description

Provides access to parameters of the screen.

## Ports

| Name        | Direction           | Type  | Binding | Description |
|:------------ |:-------------|:-----|:---|:---|
| Width | Output      |    Vector 1 | None | Screen's with in pixels |
| Height | Output      |    Vector 1 | None | Screen's height in pixels |

## Shader Function

```
float Width = _ScreenParams.x;
float Height = _ScreenParams.y;
```