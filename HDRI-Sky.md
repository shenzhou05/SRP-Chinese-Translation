Volume Component used to setup a HDRI Sky.

An HDRI Sky is a simple sky represented by a cubemap texture.

| Property      | Function                                                     |
| ------------- | ------------------------------------------------------------ |
| Hdri sky      | Cubemap representing the sky                                 |
| Sky Intensity Mode | Specify how intensity is provided                                 |
| Exposure | Intensity will be specified by an exposure and a multiplier parameter |
| Exposure      | Exposure applied to the sky                                  |
| Multiplier    | Multiplier applied to the sky                                |
| Lux    | Intensity will be specified in lux |
| Desired Lux Value | Desired Lux value for the upper hemisphere sky |
| Rotation      | Rotation applied to the cubemap in degrees                   |
| Update Mode   | Rate at which the sky environment (reflection en ambient probe) should be updated |
| On Changed    | Sky environment is updated when one of its parameter changes |
| On Demand     | Sky Environment is explicitly updated by the script          |
| Realtime      | Sky environment is updated regularly                         |
| Update Period | Period (in seconds) at which the realtime sky is updated (0 means every frame) |