Volume Component used to setup Linear Fog

Linear Fog density will increase linearly with view distance and world space height depending on the provided parameters.

| Property         | Function                                                     |
| ---------------- | ------------------------------------------------------------ |
| Density          | Global multiplier for the fog density                        |
| Fog Start        | Distance from camera at which fog density starts to increase from zero. |
| Fog End          | Distance from camera at which fog density is maximum.        |
| Fog Height Start | Height at which fog density starts to decrease               |
| Fog Height End   | Height at which fog density is zero                          |
| Color Mode       | Source of the fog color                                      |
| Constant Color   | Fog is a constant color                                      |
| Color            | Color of the fog                                             |
| Sky Color        | Fog color is sampled from the sky                            |
| Mip Fog Near     | Distance at which the blurriest sky mip is used              |
| Mip Fog Far      | Distance at which the higher sky mip (see “Mip Fog Max Mip” ) is used |
| Mip Fog Max Mip  | Maximum mip map used to sample the color (1.0 being highest resolution and 0.0 lowest resolution). |
