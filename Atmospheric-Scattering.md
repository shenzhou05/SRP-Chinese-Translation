Fog is the effect of overlaying a color onto objects dependant on the distance from the camera. This is used to simulate fog or mist in outdoor environments and is also typically used to hide clipping of objects when a camera’s far clip plane has been moved forward for performance.

In HDRP, users can choose between two different kind of fogs, linear and exponential fog. All types of materials (lit or unlit) will react correctly to the fog. Depending on the type of fog, density will evolve differently with respect to distance from camera and world space height.

Instead of using a constant color, both types of fog can choose to use the background sky as a source for color. In this case, the color will be sampled from different mip maps of the cubemap generated from the current sky settings. Chosen mip will vary linearly between the blurriest one to the highest resolution one depending on the distance from camera and the “Mip Fog” parameters. Users can also choose to limit the resolution of the higher mip used.

For both types of fog, density is computed from camera distance and world space height independently and then multiplied together to obtain the final result.

Linear Fog

Density will increase linearly with view distance and world space height depending on the provided parameters.

![img](https://lh5.googleusercontent.com/GEP6KxmxNM9uBCavFBMH_iMDR2a_v5iH8ejtCD6S7rC2gQT98sczbYeVLijxGDQE6Q_ZTGVDkNot0ietlDFMlUW2YDodnn3M1yFrsIfRVi0IdZgmxEmTss0qcGrQ074t-Zogk8fN)

| Property         | Function                                                     |
| ---------------- | ------------------------------------------------------------ |
| Density          | Global multiplier for the fog density                        |
| Color Mode       | Source of the fog color                                      |
| Constant Color   | Fog is a constant color                                      |
| Color            | Color of the fog                                             |
| Sky Color        | Fog color is sampled from the sky                            |
| Mip Fog Near     | Distance at which the blurriest sky mip is used              |
| Mip Fog Far      | Distance at which the higher sky mip (see “Mip Fog Max Mip” ) is used |
| Mip Fog Max Mip  | Maximum mip map used to sample the color (1.0 being highest resolution and 0.0 lowest resolution). |
| Fog Start        | Distance from camera at which fog density starts to increase from zero. |
| Fog End          | Distance from camera at which fog density is maximum.        |
| Fog Height Start | Height at which fog density starts to decrease               |
| Fog Height End   | Height at which fog density is zero                          |

Exponential Fog

Density will increase exponentially with view distance and world space height depending on the provided parameters.

![img](https://lh5.googleusercontent.com/HYsY9o7QzCBfDPO0q9JJindsSBHAxmw0DStEq80h4nUjSP9nItFmaIiZQCWbj_DU31RX_wV6v0YLor5va0k7aH5BOynS5J0xoJu5dSq-WuiNol7_c28J7Wby63Di50_TVPlmnhRF)

| Property               | Function                                                     |
| ---------------------- | ------------------------------------------------------------ |
| Density                | Global multiplier for the fog density                        |
| Color Mode             | Source of the fog color                                      |
| Constant Color         | Fog is a constant color                                      |
| Color                  | Color of the fog                                             |
| Sky Color              | Fog color is sampled from the sky                            |
| Mip Fog Near           | Distance at which the blurriest sky mip is used              |
| Mip Fog Far            | Distance at which the higher sky mip (see “Mip Fog Max Mip” ) is used |
| Mip Fog Max Mip        | Maximum mip map used to sample the color (1.0 being highest resolution and 0.0 lowest resolution). |
| Fog Distance           | Distance from camera at will reach maximum                   |
| Fog Base Height        | World space height at which fog density starts to decrease from 1.0 |
| Fog Height Attenuation | Fall off of height fog attenuation (bigger values will make attenuation sharper) |