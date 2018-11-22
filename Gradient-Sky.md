Volume Component used to setup a Gradient Sky.

A Gradient Sky is a simple sky represented by three colors interpolated from top to bottom.

| Property      | Function                                                     |
| ------------- | ------------------------------------------------------------ |
| Top      | Color at the top of the hemisphere                                 |
| Middle      | Color in the middle of the hemisphere                                 |
| Bottom      | Color at the bottom of the hemisphere                                 |
| Update Mode   | Rate at which the sky environment (reflection en ambient probe) should be updated |
| On Changed    | Sky environment is updated when one of its parameter changes |
| On Demand     | Sky Environment is explicitly updated by the script          |
| Realtime      | Sky environment is updated regularly                         |
| Update Period | Period (in seconds) at which the realtime sky is updated (0 means every frame) |