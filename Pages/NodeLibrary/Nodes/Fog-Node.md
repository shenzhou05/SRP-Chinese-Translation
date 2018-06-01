## Description

Provides access to the Scene's **Fog** parameters.

## Ports

| Name        | Direction           | Type  | Binding | Description |
|:------------ |:-------------|:-----|:---|:---|
| Color      | Output | Vector 4 | None | Fog color |
| Density       | Output | Vector 1 | None | Fog density at the vertex or fragment's clip space depth |

## Shader Function

```
Color = unity_FogColor;
float clipZ_01 = UNITY_Z_0_FAR_FROM_CLIPSPACE(mul(GetWorldToHClipMatrix(), mul(GetObjectToWorldMatrix(), ObjectSpacePosition)).z);
#if defined(FOG_LINEAR)
   float fogFactor = saturate(clipZ_01 * unity_FogParams.z + unity_FogParams.w);
   Density = fogFactor;
#elif defined(FOG_EXP)
   float fogFactor = unity_FogParams.y * clipZ_01;
   Density = saturate(exp2(-fogFactor));
#elif defined(FOG_EXP2)
   float fogFactor = unity_FogParams.x * clipZ_01;
   Density = saturate(exp2(-fogFactor*fogFactor));
#else
   Density = 0.0h;
#endif
```