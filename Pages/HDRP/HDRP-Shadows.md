# Shadow quality

## Shadow [atlas](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Glossary#TextureAtlas)

In HD render pipeline, all the realtime shadows rendered for a frame are stored in two different shadow map atlases. The first one is used for all punctual shadows (spot and point lights) and have the possibility to rescale his shadow maps if too many of them are rendered and would not fit in the atlas. The second is used for directional shadow cascade and don't rescale.

The size of these atlases are set in the HDRenderPipeline asset and it determines the maximum resolution you'll be able to have for a shadow.

For instance the default size of the atlas is 4096 x 4096 and so it can fit 4 shadow maps of 1024 x 1024 pixels, or 2 shadow maps of 1024 x 1024 + 4 shadow maps of 512 x 512 + 16 shadow maps of 256 x 256.

## Shadow Requests
In addition to the atlas, to manage the budget of your shadows, in the HDRenderPipeline asset you can set the "Max Shadow Requests" to limit the maximum shadow maps rendered in a frame. This number is directly used to allocate shadow data compute buffer so if the number of shadow maps on your screen is higher than this limit, they will not be rendered.

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
They are exposed in the HDRenderPipeline asset as shadow quality (low, medium and high) and can be choosed for directional and punctual lights.

Quality     |   Current algorithm
|-----------|------------------------|
Low | PCF 3x3 (4 taps)
Medium | PCF 5x5 (9 taps)
High | PCSS (sample count can be set by light in the light component)

# ShadowMasks

ShadowMasks is one of the Mixed Lighting modes available in Unity.
If you are not familiar with mixed lighting modes you can check out the [documentation](https://docs.unity3d.com/Manual/LightMode-Mixed.html).

HD Render Pipeline only supports mixed mode **Baked indirect** and **Shadowmask**.

## Enabling shadow masks

In order to enable Shadow masks in HD Render Pipeline, one needs to enable Shadow masks support on the HDRenderPipeline Asset in 2 different places :

- In Render Pipeline Settings enable "Support Shadow Mask"
- In Default Frame Settings under the Lighting Settings tick "Enable Shadow Masks"

Also one should make sure that in the project's quality settings the **Shadowmask Mode** is set to **Distance Shadowmask**.

## Specific settings in HD Render Pipeline

In HD Render Pipeline, in order to give more flexibility to the Shadowmask mixed lighting mode, we allow you to choose on each light how you want the ShadowMasks to behave.
This behavior is mainly influenced by the checkbox : **Non Lightmapped Only** that is located on the **Light component**, under **Shadows** when the light **Mode** is set to **Mixed**.

**Non Lightmapped Only** 
- when this is **disabled**, the light will cast a **realtime shadow** for all objects **when the distance between the camera and the light is inferior to the Shadow fade distance**. When distance between the light and the camera is bigger than the **Shadow fade distance**, the light will stop calculating realtime shadows. It will use the shadowmask for static objects shadow and non static objects will not cast shadows anymore. 
- when this is enabled, the light will cast a **realtime shadow** for non static objects only and combine it with the Shadowmask for static objects **when the distance between the camera and the light is inferior to the Shadow fade distance**. When distance between the light and the camera is bigger than the **Shadow fade distance**, the light will stop calculating realtime shadows. It will use the shadowmask for static objects shadow and non static objects will not cast shadows anymore.

**For the directional light**, the **Shadow fade distance is replaced by the Max Distance** located on the **HD Shadow Settings** Volume component.

**The first behavior requires more GPU power** but Shadowmask textures can have a low resolution because they will only be used at a certain distance.

**The second behavior requires more memory** since Shadowmask textures will be used when the camera is nearby and the Shadowmask textures resolution will likely need to be bigger.

# Contact shadow

Contact shadows are shadows raytraced in screen space on a short distance in order to provide small detailed shadows for small details in geometry that shadow maps cannot usually capture.

Currently, contact shadows are rendered for one light at a time.

In order to enable contact shadows you need to :

- Got to your HDRenderPipeline Asset and make sure under "Lighting Settings" that "Enable Contact Shadows" is ticked
- In one of your loaded scenes you need to have a Contact Shadows Volume component on an active Volume with the "Enable" box ticked
- On the light you choose for casting contact shadows, enable "Shadows" and "Show Additional Settings", and then under "Shadows" section tick "Enable Contact Shadows"

:warning: Only one light can cast contact shadows at a time, it means that if you have more than one light that cast contact shadows visible on the screen, only the dominant light will render contact shadows. The dominant light is chosen using the screen space size of the bounding box of the light (note that if you enable contact shadows on the directional light, it'll always be the dominant light).

More details : [Contact shadows](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/HD-Contact-Shadows)