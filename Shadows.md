This page is wip and incomplete at the moment

# Shadow quality

## Shadow atlas

In HD render pipeline, all the realtime shadows rendered for a frame are stored in a shadow map atlas.

The size of this atlas is set in the HDRenderPipeline asset and it determines the shadow budget for a frame.

For instance the default size of the atlas is 4096 x 4096 and so it can fit 4 shadow maps of 1024 x 1024 pixels, or 2 shadow maps of 1024 x 1024 + 4 shadow maps of 512 x 512 + 16 shadow maps of 256 x 256.

## Shadow map resolution

The resolution of the shadow map determines how big will be the shadow map(s) rendered for a light. The bigger is a shadow map, the more precise it can be, and the best it can capture small details in the shadow casting geometry. A shadow map rendered at high resolution will also look sharper.

The resolution of the shadow map(s) rendered for a light is set on the Light component under the Shadows section.

The number of shadow maps rendered per light depends on the type of the light :

- A spotlight will render 1 shadow map
- A point light will render 6 shadow maps (like the number of faces in a cubemap)
- A directional light will render one shadow map per Cascade. The cascade count is set in the Volume component HD Shadow Settings. The default value is 4 cascades. For more details on Cascaded shadow maps refer to the HD Shadow Settings Volume component page.

## Shadow Bias

Since shadow maps are like textures projected from the point of view of the light, we need to use a bias in the projection so that the shadow casting geometry does not get self shadowed in the end.

In HD Render Pipeline the shadow biasing is controlled by several parameters in the Light component under the Shadow Section.

**View Bias Scale :**

**Normal Bias :**

## Shadow filtering

Core Render Pipeline comes with several shadow map filtering algorithms. HD Render Pipeline allows users to use some of these algorithms in order to smooth the shadow maps.



# ShadowMasks

ShadowMasks is one of the Mixed Lighting modes available in Unity.

## Enabling shadow masks

In order to enable Shadow masks in HD Render Pipeline, one needs to enable Shadow masks support on the HDRenderPipeline Asset in 2 different places :

- In Render Pipeline Settings enable "Support Shadow Mask"
- In Default Frame Settings under the Lighting Settings tick "Enable Shadow Masks"

## Specific settings in HD Render Pipeline

In HD Render Pipeline, in order to give more flexibility to the ShadowMasks mixed lighting mode, we disabled the Quality Setting "shadow masks mode" so that you can choose on each light how you want the ShadowMasks to behave.

# Contact shadow

Contact shadows are shadows raytraced in screen space on a short distance in order to provide small detailed shadows for small details in geometry that shadow maps cannot usually capture.

Currently, contact shadows are rendered for one light at a time.

In order to enable contact shadows you need to :

- Got to your HDRenderPipeline Asset and make sure under "Lighting Settings" that "Enable Contact Shadows" is ticked
- In one of your loaded scenes you need to have a Contact Shadows Volume component on an active Volume with the "Enable" box ticked
- On the light you choose for casting contact shadows, enable "Shadows" and "Show Additional Settings", and then under "Shadows" section tick "Enable Contact Shadows"

For more details on the Contact shadow settings refer to the Contact Shadow volume component page.