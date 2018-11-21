This section of the documentation is still in progress. For more information, or to ask questions about this topic, please visit the [High Definition Render Pipeline forum](https://forum.unity.com/forums/graphics-experimental-previews.110/).

## Reflection Probe

### Manual

#### HDRP Settings

#### Reflection probes volumes

##### Proxy volume

##### Influence volume

The influence volume defines which pixels will use the lighting from this probe.

![img](https://docs.google.com/a/unity3d.com/drawings/d/smHHyJCNXHJfMxt3_ev7nFQ/image?w=624&h=587&rev=1&ac=1&parent=1skprpTeWm7xJWnUbRXU1AFL9pDK3PSSIUPhABPH5vZ0)

##### Blend influence volume

The blend influence volume defines a blending distance from the influence volume and weight the influence of the probe accordingly.

 

Commonly use to fade the influence between multiple probes.

![img](https://docs.google.com/a/unity3d.com/drawings/d/s6tmGas6fJLFHD4oo55KZbg/image?w=624&h=439&rev=1&ac=1&parent=1skprpTeWm7xJWnUbRXU1AFL9pDK3PSSIUPhABPH5vZ0)

##### Blend normal influence volume

A pixel outside of the blend normal influence volume will received a blended influence from the probe.

If this pixel has a normal pointing outwards the capture position, it won’t receive any influence from this probe.

![img](https://docs.google.com/a/unity3d.com/drawings/d/smXs9P74WjtwTD9Pk-smD6g/image?w=624&h=446&rev=1&ac=1&parent=1skprpTeWm7xJWnUbRXU1AFL9pDK3PSSIUPhABPH5vZ0)

#### Reflection Probe Inspector

[Insert screenshot]

##### Primary fields

##### Edit modes

- Influence
- Blend
- Blend normal
- Capture position

##### Proxy volume

Important notice: The influence volume and the proxy volume must have the same shape type.

##### Influence volume fields

##### Capture settings

##### Additional Settings

##### Action Toolbar

#### Cubemap Inspector

[Insert screenshot]

 

- Mip slider
- Brightness slider
- Mouse rotate
- Mouse zoom

#### Debug Tools

### Baking Workflow

#### Baked

#### Custom

#### Realtime

### Scripting

#### Trigger bake

#### Trigger custom bake

#### Render a probe

## 

## Planar Reflection Probe

### Manual

#### HDRP Settings

#### Planar probes volumes

##### Proxy volume

Important notice: The influence volume and the proxy volume must have the same shape type.

##### Influence volumes

See influence volumes of Reflection Probes.

 

#### Planar Probe Inspector

![img](https://lh4.googleusercontent.com/6UXWmLNSc0wd1Y8n-JcsP3ENCTez9PVv2t_iprtO-BkldCXy-6-gbxJJHZL0r8riYOCFy3VoM2Vuhc_h-ffL5m3QC4eNgAkJouwKTLALUkNLuqlVy21pklkrXbT4ljVJ4l3C77Tv)

##### Primary fields

Only one workflow is supported for planar probe, so it can’t be modified.

(Realtime, Every Frame, Mirror Camera)

##### Edit modes

##### ![img](https://lh6.googleusercontent.com/vEe1BBF68Zp_vOVJK7crLJA4T_B9N-vC1ENWSuLOiVUOX6IWp2Uwk9CgUUqqCaFvXbODSlrNeLdduJlQrK7F3yU7KQ1DizJHw0ZquE8YdG2kTkQyd5kwvdE3ym_tbA2h3-ulvjpr)

 

| 1. Influence volume editingEdit the bounds of the influence volume. ![img](https://lh6.googleusercontent.com/V79cCV7luxG8G-DhL5nHWf1n8HXVpRWiyhKovLpxkQUNvOrBx1Ubzw17wWQWjLD9O-Z5HAYcdA50xiD7zn4fc4bx_JWFXL5A4jVw9k89QE4wfc42jIWTB4XgRIfPmuZPTTnocqZR) | 2. Blend influence volume editingEdit the bounds of the blend influence volume.![img](https://lh6.googleusercontent.com/4Xu4yH2DYDO4YWV8AdZ2I-b2UvEPC6qChz8Mr001WfpNtkJcY0c90ckh0MWD20YbE7Qfj_nFPCmkKHrZYIlrDO4Krz4o_WTX7Hs6vlkyOVhcYltell-KLqD6Vb5uU0EWh-JYxbxs) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 3. Blend normal influence volume editingEdit the bounds of the blend normal influence volume.![img](https://lh4.googleusercontent.com/j9hunBLE0A3FQVdwqziNVUeDaMshH4_KG70jfKcIPP967JKleQNa0wb4o7awAQvFpRssB_o5mYJqSgtKmP6soAaEw2pzni9Dw0dLeCib4aTuImHBpbf9vYG6xd6MjI2E5fdOIKlk) | 4. Mirror plane position editingEdit the position of the mirror plane. ![img](https://lh3.googleusercontent.com/DlQnKKDrQcvm63YD1zZeA496nHFnFK7rbgOHIz4lFm-i-7u2aWymO0Qa6EhWEfCyG6I_OYDZnKLVWt2pSuU9jBmSHAlIVMrPIvWgL_ecsZePyc1hztsuN7IcYOhms19vXEZWLgXj) |
| 5. Mirror plane rotation editingEdit the rotation of the mirror plane.![img](https://lh4.googleusercontent.com/Re0n4CV-Rvqx0VX1nhG3CvQly9P2bHo5jPQQUatc-iEzOz-W7zNP9Umqmn7OAX7w5cCRwgdXvNvOlh68qYh5VrM49MHK-BhL9dx0OykKDhtptPHAvmbPrqb4Iqv2rzD-TZyDwGUQ) |                                                              |

##### Proxy volume

Choose the proxy volume component (ReflectionProxyVolumeComponent) to use.

If none, an infinite projection will be used.

##### Influence volume fields

###### Box shape

 

| Box Size                            | Size of the box                     |
| ----------------------------------- | ----------------------------------- |
| Box offset                          | Offset of the center of the box     |
| Influence fade (per axis)           | Blend the influence per axis        |
| Influence normal fade (per axis)    | Blend the influence normal per axis |
| Influence face fade (per cube face) | Blend the influence per cube face   |

###### Sphere shape

 

| Radius                | Radius of the influence    |
| --------------------- | -------------------------- |
| Influence fade        | Blend the influence        |
| Influence normal fade | Blend the influence normal |

 

##### Influence settings fields

 

| Weight     | A weight for this probe influence     |
| ---------- | ------------------------------------- |
| Multiplier | A multiplier for this probe intensity |

 

##### Capture settings

 

| Override FOV  | Whether to override the capture camera fov    |
| ------------- | --------------------------------------------- |
| Field of view | Field of view to use when capturing the probe |

#### Render settings

Include the render settings of the capturing camera.

#### Debug Tools

### Baking Workflow

#### Baked

N/A

#### Custom

N/A

#### Realtime

### Scripting

#### Trigger bake

N/A

#### Trigger custom bake

N/A

## Render a probe

### FAQ

#### My planar probe does not reflect anything.

Follow these steps:

1. Is the influence volume correct?
   It should overlap with the reflecting objects.
2. Is the mirror plane properly placed?
   The mirror plane should be placed on your reflecting surface and the normal of the mirror plane must be parallel with the normal of the reflecting surface.
   Try editing its position and rotation with the toolbar in the Planar Probe’s inspector.