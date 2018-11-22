Volume Component used to setup a Procedural Sky

This sky is similar to the procedural sky provided with the built-in Unity Render Pipelines. 

| Property              | Function                                                     |
| --------------------- | ------------------------------------------------------------ |
| Enable Sun Disk       | Display sun disk                                             |
| Sun Size              | Size of the sun disk                                         |
| Sun Size Convergence  |                                                              |
| Atmospheric Thickness |                                                              |
| Sky Tint              | Color of the sky hemisphere                                  |
| Ground Color          | Color of the ground hemisphere                               |
| Exposure              | Exposure applied to the sky                                  |
| Multiplier            | Multiplier applied to the sky                                |
| Update Mode           | Rate at which the sky environment (reflection en ambient probe) should be updated |
| On Changed            | Sky environment is updated when one of its parameter changes |
| On Demand             | Sky Environment is explicitly updated by the script          |
| Realtime              | Sky environment is updated regularly                         |
| Update Period         | Period (in seconds) at which the realtime sky is updated (0 means every frame) |