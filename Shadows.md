This page is wip and incomplete at the moment

# Shadow quality

## Shadow atlas

In HD render pipeline, all the realtime shadows rendered for a frame are stored in a shadow map atlas.

The size of this atlas is set in the HDRenderPipeline asset and it determines the shadow budget for a frame.

For instance the default size of the atlas is 4096 x 4096 and so it can fit 4 shadow maps of 1024 x 1024 pixels, or 2 shadow maps of 1024 x 1024 + 4 shadow maps of 512 x 512 + 16 shadow maps of 256 x 256.

## Shadow resolution

The resolution of the shadows cast by a light is set on the light itself under the Shadows section.

The number of shadow maps created per light depends on the type of light :

- A spotlight will create 1 shadow map
- A point light will create 6 shadow maps (like the number of faces in a cubemap)
- A directional light will create one shadow map per Cascade. The cascade count is set in the Volume component HD Shadow Settings. The default value is 4 cascades.

## Shadow filtering

Core Render Pipeline comes with several shadow map filtering algorithms. HD Render Pipeline allows users to use some of these algorithms in order to smooth the shadow maps.



# ShadowMasks

ShadowMasks is one of the Mixed Lighting modes available in Unity.

## Enabling shadow masks

In order to enable Shadow masks in HD Render Pipeline, one needs to enable Shadow masks support on the HDRenderPipeline Asset.

## Specific settings in HD Render Pipeline

In HD Render Pipeline, in order to give more flexibility to the ShadowMasks mixed lighting mode, we disabled the Quality Setting "shadow masks mode" so that you can choose on each light how you want the ShadowMasks to behave.

# Contact shadow

Contact shadows are shadows raytraced in screen space on a short distance in order to provide small detailed shadows for small details in geometry that shadow maps cannot usually capture.

Currently, contact shadows are rendered for one light at a time.

In order to enable contact shadows you need to :

- Have a Contact Shadows Volume component on an active Volume with the "Enable" box ticked
- On the light you choose for rendering contact shadows, enable "Shadows" and "Show Additional Settings", and in the "Shadows" section tick "Enable Contact Shadows"