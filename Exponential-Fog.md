# Exponential Fog

Volume Component used to setup Exponential Fog

Exponential Fog Density will increase exponentially with view distance and world space height depending on the provided parameters.

| Property               | Function                                                     |
| ---------------------- | ------------------------------------------------------------ |
| Density                | Global multiplier for the fog density                        |
| Fog Distance           | Distance from camera at will reach maximum                   |
| Fog Base Height        | World space height at which fog density starts to decrease from 1.0 |
| Fog Height Attenuation | Fall off of height fog attenuation (bigger values will make attenuation sharper) |
| Color Mode             | Source of the fog color                                      |
| Constant Color         | Fog is a constant color                                      |
| Color                  | Color of the fog                                             |
| Sky Color              | Fog color is sampled from the sky                            |
| Mip Fog Near           | Distance at which the blurriest sky mip is used              |
| Mip Fog Far            | Distance at which the higher sky mip (see “Mip Fog Max Mip” ) is used |
| Mip Fog Max Mip        | Maximum mip map used to sample the color (1.0 being highest resolution and 0.0 lowest resolution). |
