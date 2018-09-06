# HDRP Sky

## Setting up the Sky

Setting up a sky has two goals: The first one is to define what will be displayed in the background of the scene for a given camera. The second one is to define environment lighting, namely sky reflection and sky ambient probe which is then later used to render lightmaps (real-time or baked).

Settings are split between global settings which are per project/platform and local settings that use the volume framework and can change depending on the scene or camera position.

## Global Sky Settings

Global settings for the sky are in the HDRenderPipeline configuration asset:

![img](https://lh5.googleusercontent.com/lsQ4lmXDAnlJwx96D4OZEHTGd3rF0CSlqK4t0WIEx6BgToV-uD2ecrFlCKB0_DDPpkSFgv8D-hIb_kUREZSj0_eelNXyDVOaILGCCpR11CM-eseyf5tfpUnblcvd68mvbwXUl3PO)

Sky Reflection Size

This parameter drives the size of the cubemap generated from the sky and used for fallback reflection when no local reflection probes are present. It has no effect on the quality of the sky rendered in the background.

Sky Lighting Override Mask

In some cases, users may want to dissociate lighting environment from what is rendered in the background (a typical example is to have a very dark sky at night but have a brighter lighting so that the player can still see).

In order to achieve this, users can define the sky lighting override mask which is a Layer mask. If any volumes are present in this layer then environment lighting will use these volumes instead of those from the main camera. If this mask is set to Nothing or if there are no volume in this mask then lighting will come from volumes setup in the main camera volume layer mask.

In practice this means that user can define two sets of masks, one for the visual sky and the other for the lighting. Both sets of volume will then be interpolated independently from each other.

Note that lighting override does not affect baked lighting.

## Local Sky Settings

Once global parameters are set, users need to setup volumes with the correct components to setup local parameters for the sky. Currently HDRP provides two different kind of skies.

Procedural Sky

This sky is similar to the procedural sky provided with the built-in Unity Render Pipelines. 

![img](https://lh4.googleusercontent.com/IKb-5rlvHrZJJlfX6qAHWZngnHm0jCEE8ZYpvMySWihyekwhgONTBj4VkIAWBSKHfFOsPEISPbaLQpAgOr3vQYPx3oAsq4Ei_y7rxuRaXA0FSZpIh2G_chsnl_j4RjaqA3CGjdgD)

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

HDRI Sky

Simple sky represented by a cubemap texture.

![img](https://lh5.googleusercontent.com/DD0NrAEKp3l9D5gyodSMCQ2vgg-jAQzWd8u7hBGSDlVgS6vceMyU69YYvemH4NXNzzXwbTwiNkgRYLobpmiv9lt4u1tAT02SQyUJuQe3zwL6NU1HNYs1YzRE3BNSVneq7d9HD9hq)

| Property      | Function                                                     |
| ------------- | ------------------------------------------------------------ |
| Hdri sky      | Cubemap representing the sky                                 |
| Exposure      | Exposure applied to the sky                                  |
| Multiplier    | Multiplier applied to the sky                                |
| Rotation      | Rotation applied to the cubemap in degrees                   |
| Update Mode   | Rate at which the sky environment (reflection en ambient probe) should be updated |
| On Changed    | Sky environment is updated when one of its parameter changes |
| On Demand     | Sky Environment is explicitly updated by the script          |
| Realtime      | Sky environment is updated regularly                         |
| Update Period | Period (in seconds) at which the realtime sky is updated (0 means every frame) |

## Baking Global Illumination with the sky

In HDRP the sky is completely controlled by the volume system. It means that in the editor, the current state of the sky will depend on the camera position. The consequence is that for users to get a consistent lighting baking, we can’t rely on what is in the scene.

Instead the sky used for baking is set explicitly by the user through the Baking Sky component.

![img](https://lh4.googleusercontent.com/-z7fJzda_xSO5NEE8BxL6iJZO1s93ECvIzOXwB2rujcLJAbMquAJQhN0zKhtmZ6Y4KALSiqn14jWxu292AQyO59yKgsFsV485EpIt1z1aSu-_FXyl1-AmTP_oeAaAq7E1SVCWgGJ)

User should select a volume profile which contains the sky intended to be used for baking and then choose the right type (in case the profile contains different kinds of skies). If the component is added to a game object that already has a Volume, the profile property will be automatically populated with the corresponding profile asset.

This sky setting will live outside of the volume framework and thus will never be interpolated based on the camera position. Any time the baking is required, this is the sky that will be used.

Only one such component can be present in the editor at any given time. Any additional component of the same type will generate a warning and be ignored.