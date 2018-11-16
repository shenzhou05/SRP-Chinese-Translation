# What is Subsurface Scattering?

By definition, **Subsurface Scattering (SSS)** is light transport within the participating media under the surface.
In practice, it makes organic materials such as skin look smooth and natural rather than rough and plasticy.
The **HD Render Pipeline (HDRP)** implements the **SSS** effect using a screen-space blur technique.

SSS is also responsible for the translucent look of back-lit objects that allow a portion of light to penetrate (be transmitted through) them. For certain types of objects, performing the blur pass may not make a large visual difference. Therefore, the **HDRP** implements two material types: the **Subsurface Scattering** material type implements both the screen-space blur and transmission (the latter can be disabled), while the *Translucent* material type only models transmission.

# Enabling Subsurface Scattering

**SSS** can be toggled in the **HDRP Asset**.

![SSS Settings in the HDRP Asset](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/0bb926eeb876793dc58da1ce8048f4b5e6525424/com.unity.render-pipelines.high-definition/Documentation~/Images/sss_hd_asset.png)

- In your **HDRP Asset** under **Supported Features** check the **Subsurface Scattering** option.
- Optionally, just below, you may choose to **Increase the SSS Sample Count**. This can potentially reduce the amount of visual noise (due to undersampling) produced by the blur pass at roughly 2.5x the cost, so make sure you can afford it.
- Still in the **HDRP Asset**, locate the **Default Frame Settings**. Under **Lighting Settings**, make sure that both **Subsurface Scattering** and **Transmission** are enabled.

