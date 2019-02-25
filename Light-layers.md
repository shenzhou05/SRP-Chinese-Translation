In order to use this feature, make sure **Light Layers are enabled in your HDRP asset**. 
Also check that your **default frame settings for Camera** have Light layers enabled.

**Using light layers :**
- Select a light
- In the General category click the "Advanced settings" button ("+" icon in the header)
- In the light layer field select one or more light layers
- Select a mesh renderer
- Open the "Rendering layer mask" dropdown and select the combination of layers you want for this object

If any layer matches between light and mesh renderer, the mesh will be lit by this light.

This section of the documentation is still in progress. For more information, or to ask questions about this topic, please visit the [High Definition Render Pipeline forum](https://forum.unity.com/forums/graphics-experimental-previews.110/).