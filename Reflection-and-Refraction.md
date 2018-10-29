# Reflection

There are several techniques used to calculate reflections in HD Render Pipeline : **Sky reflection probe**, **Local Reflection probes**, **SSR **(or Screen Space Reflections), **Planar reflection probes**. These different techniques have variable **runtime cost**, **editing cost**, and **accuracy**. Depending on your target platform and the amount of time you can spend on the setup, you can decide to use all of these techniques, or only some of them.

## Reflection hierarchy

In order to have the best reflections, HD Render Pipeline needs to select which of the reflection techniques available gives the best accuracy for each pixel and use that for calculating reflections, while ensuring it blends with all the other techniques.

The selection of the best reflection for a given pixel is done in a certain order that we call **Reflection hierarchy**. If the technique at the first level of the hierarchy doesn't contain valuable information for the pixel, we fallback to the next technique in the hierarchy, and so on until we find good information or until we reach the ultimate fallback technique which is **Sky reflection probe**.

The reflection hierarchy order is :

1. **Screen Space reflection** (Opaque only)
2. **Standard & Planar probe reflections**
3. **Sky reflection**

## Screen Space Reflection

The Screen Space Reflection is available only for opaques objects. 

It uses the depth and color pyramids from the previous frame.

 

To configure the Screen Space Reflection add a “Screen Space Reflection” component override in the Volume Component.

### Screen Space Reflection Settings

#### Common Settings

 

| Screen Weight Distance | The screen weight distance is a blending applied when the fetched color is near the boundaries of the screen. (In NDC coordinates) Example for a weight of 0.1:The x coordinate will fade as  X          : 0 -> 0.1 -> 0.9 -> 1.0  Weight : 0 -> 1.0 -> 1.0 -> 0.0 |
| ---------------------- | ------------------------------------------------------------ |
| Projection Model       | Projection model to use (Proxy, HiZ) NB: HiZ is not currently available |

 

#### Proxy projection model

![img](https://lh5.googleusercontent.com/q6BoxBLiQms2KgQGoOCN6E9UrvhSTVbe1psaYVTXEgvKVO4ZvDMohjgK3ZiBp9EnKhGQgJDJ7nWlZgv2RlK4QkldxEoRXp5STZnHA6fONqx8OY30LwHVOdJ0ds4BrLW4V7M66738)

 

No additional parameters

#### HiZ projection model

![img](https://lh5.googleusercontent.com/lsU5aby6atdKogPIGMr4lgsy_1w9jWx03Gi5GiugdLSvcm1O42-KaMrEk_qgF9cvmVdFrut5I7W-0_LjBByCibA8QuAeVHl1zzQCPFAqJMNyfEplW9f7C8hbqgsT88wJgqHK1DTh)

 

 

| Ray min level          | The minimum mip to use. The lowest, the most accurate and the most costly. |
| ---------------------- | ------------------------------------------------------------ |
| Ray max level          | The maximum mip to use. The lowest, the most accurate and the most costly. NB: If this parameter is too high, artifacts may appears |
| Ray max iterations     | Maximum number of iterations before failing. Use this parameter to cap the cost of this algorithm. |
| Ray depth success bias | Bias to use when checking when the ray is marching behind an object. |

 

### Debugging

![img](https://lh5.googleusercontent.com/waGTC_bWZNoTcXFaYsT4iG9OpL0RFC_7R0Nx1oapx5v8tk9kmv9mRUB_cb9laJSbKSvV-psWtXd9P_ZEYy42Npi6ltxMr1qVf_eMjdCSTeVSCE1_5eWAkYdzqfCjSLwcyiY-Higc)

#### Pixel debugging

Click in the view to select a pixel, you will see the queried ray on the screen and the associated information will be displayed in the debug window.

 

NB: in forward, the debug show the information of the last drawn object and may not be the object you think.

NB: You can press “Home” and mouse your mouse to update the debugged pixel position, So you want interact with the scene while debugging.

 

![img](https://lh3.googleusercontent.com/1sJuruwytcYcnljMDpN1GPnzoTHD11Wj-T4JEd3ASH5W49daIkuwZKMd5DqBKLwx5CioC7nBJcVi68Mzkrjc2ET325d_D0cX5llgNysIIk0wse4RDfHbxXPyH11ux9Z1Stg9KlnU)

 

The debug information are specific to a projection model and are available once a pixel is debugged.

 

##### Proxy projection model

 

| Hit success         | Whether the ray successfully hit the proxy and is in front of the camera. |
| ------------------- | ------------------------------------------------------------ |
| Proxy Shape         | The proxy shape used for the raycast                         |
| Projection Distance | The distance between the hit and the ray origin              |
| Start position      | Ray origin (screen space)                                    |
| Start linear depth  | Linear depth of the ray origin                               |
| End linear depth    | Linear depth of the hit                                      |
| End position        | Position of the hit (screen space)                           |

 

###### Debug modes

 

| Color Show the color output of the lighting.                 | ![img](https://lh3.googleusercontent.com/aONLRL2ry80bweNdkZ2fb98P9YJ7bAhJ4e3vrXTUT9Ws84rWAZvtnSYBCVZMa1KJZkn-up763cRtvzm7KEZ6409bTvsCZyQsWCihQzjxd8tZCh8ZLcM8tXs_u0EEO2h1_X49ewD4) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| RayDirWS Show the ray direction in world space.              | ![img](https://lh6.googleusercontent.com/M-mojT9X8t5iIscuMS8cL1Ds_6wjnNI6DkMY5OOOS8brRWoNpC0V3F2cu6NbGrCAVq3NYrc9k2W0IX07RCJgUjLZe6FmxCuBENj2cn-5paVCz-9OY8XTS6b8A195Al3FoIQd3-jA) |
| HitDepth Show the depth of the hit.                          | ![img](https://lh4.googleusercontent.com/_FhB0YvDVPSDYPQRmn47bT6PLESr-VDexhXwDy_zDckb7QM_as64GgjRFo3BsyJcacAOMVbpQr3_h-PKhb1bAQFhfegtFbvkYQzlsJN9n29rK-iXtjUEYuBqLX-usRldgZ2G2Xdz) |
| HitSuccess Show whether the ray successfully hit the proxy and the hit point is in front of the camera. Light green  : Hit successLight blue    : Hit failedOther           : No raycast | ![img](https://lh3.googleusercontent.com/EYEjGUCwl4pRbygSNbVOP8CkD2CgddZ2OhFj5_o_SlZe_a6yfHBsWHFy64OC5HrZuVvY2VeSQWCTabrFZM9JZpUCiuX9UZ8fvhbgqS5FzpY2xayN4AEkao0nRzRuQFUdFOKHCczn) |

 

## 





# Refraction

## Refraction Hierarchy

(SSRefraction => reflection probe => sky)

## Refraction Theory

We will simulate the light deviation and absorption in our refraction algorithm.

So, we need to compute the light deviation and the distance of the light within the material.

 

We assume that the light will go through: air -> material -> air.

So we need to calculate the deviation at both of the material interfaces (air -> material and material -> air).

 

In order to speed up computation, we assume that the surface of the object can be approximated locally by a simple shape. We name the shape model “Refraction Model”.

 

Once we have the local shape, we are able to compute the light deviation and the distance of the light within the material.

 

We now need to find the hit of the deviated light ray and get the color of that point. To do so, we will use a “Projection Model”.

 

We will use this standard for the naming:

p:object hit position

n⃗:object normal

t:model thickness

 

Basic description:

- Refraction model
- Raycasting & projection
- Color sampling

### Refraction model

#### Sphere

We approximate the surface as a sphere with the following parameters:

csphere center=p-n⃗*t*0.5

rsphere radius=t*0.5

 

![img](https://docs.google.com/a/unity3d.com/drawings/d/sOzCUi8eTvEw7QzQpHUUInA/image?w=624&h=492&rev=1&ac=1&parent=1skprpTeWm7xJWnUbRXU1AFL9pDK3PSSIUPhABPH5vZ0)

#### Plane

We approximate the surface as a thick plane with the following parameters:

cplane center      =p-n⃗*t*0.5

wplane thickness =t

![img](https://docs.google.com/a/unity3d.com/drawings/d/sgeSI81wJB4qCfFuJU2BMag/image?w=624&h=499&rev=1&ac=1&parent=1skprpTeWm7xJWnUbRXU1AFL9pDK3PSSIUPhABPH5vZ0)

#### Common use case

- For filled object, you should use a Sphere model with a thickness approximating the size of the object.

![img](https://lh3.googleusercontent.com/jIq16k-lctRba5xVV-LH0CmrrJs6D6-JsZBdZIdo5UWNYfZaZlhvo7ZepNpT30DE3mmX2ZFUjA3o_EzRBrUdx8oYcrQLH033ZlYhe0EGrZwBTvwcUluifBggdCf-d5aYbLh9BpgJ)

- For an empty object, you should use a Plane mode with a small thickness.

### ![img](https://lh6.googleusercontent.com/eynOF-SdQ0ryREgGuY4O99P4Uv9cpoz545Fs4gasvsX0IyFyhKOIrMmt-Pgun26kBq4ER5UQAkQw6a1HmjQGnIkujkFxwPBwkK3Z05n4261TdKr_Bb9-g6aH80xMmw-mTfC_lMuy)

### Projection model

See [Appendix - Projection models](https://docs.google.com/document/d/1skprpTeWm7xJWnUbRXU1AFL9pDK3PSSIUPhABPH5vZ0/edit#bookmark=id.c3zmas14ei6w)

#### Proxy

We approximate the scene by a simple shape and then perform a raycast against this shape the compute the deviated light ray hit.

 

SUBJECT TO CHANGE IN FUTURE VERSION

Currently the proxy used for the computation is:

1. The proxy associated to the first environment light found for this pixel (either Reflection probe or Planar probe)
2. If none, the sky’s proxy will be used (equivalent to an infinite projection)

END

#### HiZ (Preview)

We perform an accelerated raymarching in the depthbuffer by using a HiZ depth pyramid.

### Absorption

When the transmittance color is not white, then the light is attenuated depending on the distance of the light ray within the material.

The greater the distance, the more attenuated the light is.

 

![img](https://lh4.googleusercontent.com/Zhd68CiRHiUfw6cst_EurRgLDzLidTPJAEnW63dMmKryTeFdCHbpSdnYc0EBxf7-LzkIA3jJVkvEqygHnF1xQmpHvYv5tHo4urOg7TgHS_umtKRmWeCl2TVXpf1fMcf0HJ2xBLeD)

Transmittance Absorption Distance from 0 (top right) to 6 (bottom left)

## Refraction Settings

### Material Settings

 

| Refraction model                  | Define the refraction model to use.Set to None to disable refraction |
| --------------------------------- | ------------------------------------------------------------ |
| SSRay Model                       | The Projection model to use                                  |
| Index Of Refraction               | The IOR to use for this material.                            |
| Refraction Thickness              | The thickness to use for the refraction model                |
| Refraction Thickness Multiplier   | A multiplier for the thickness.                              |
| Transmittance Color               | This is the colors that can goes through your transparent. So if you set it to red, the more thick your transparent is, the more green and blue are absorbed. |
| Transmittance Absorption Distance | This is the approximately the thickness where your object will have the ‘Transmittance Color’ from white light. |

### Volume Settings

#### Common Settings

 

| Screen Weight Distance | The distance in NDC to blend the screen space effect. Use this parameter to blend the screen space effect with the fallback when the sample is near the border of the screen buffer. |
| ---------------------- | ------------------------------------------------------------ |
|                        |                                                              |

 

#### HiZ Settings

 

| Ray Min Level          | Minimum mip level to use in the HiZ buffer                   |
| ---------------------- | ------------------------------------------------------------ |
| Ray Max Level          | Maximum mip level to use in the HiZ buffer                   |
| Ray Max Iterations     | Maximum iterations for the HiZ                               |
| Ray Depth Success Bias | Bias to use when checking if the ray is behind the current depth buffer value. |

 



# Appendix

## Projection models

A projection model is used to compute a raycast hit against scene geometry.

Each model is based on a specific resource set and is designed to match a resource budget.

### Proxy raycasting

You can define a scene proxy with the [ReflectionProxyVolumeComponent](https://docs.google.com/document/d/1skprpTeWm7xJWnUbRXU1AFL9pDK3PSSIUPhABPH5vZ0/edit#bookmark=id.z8l42xos9tm3).

 

When performing a raycast, we will raycast against the shape defined in the [ReflectionProxyVolumeComponent](https://docs.google.com/document/d/1skprpTeWm7xJWnUbRXU1AFL9pDK3PSSIUPhABPH5vZ0/edit#bookmark=id.z8l42xos9tm3).

 

It requires only one depth buffer sample and the projection error is the difference between the proxy volume and the actual scene geometry.

 

Example of a proxy projection during a reflection:

 

![img](https://docs.google.com/a/unity3d.com/drawings/d/s0tRTxi4UQXybPbCyj6oFXw/image?w=380&h=351&rev=1&ac=1&parent=1skprpTeWm7xJWnUbRXU1AFL9pDK3PSSIUPhABPH5vZ0)

### HiZ raymarching (Preview)

When using HiZ, we raymarch a depth pyramid to calculate the hit.

 

It is based on screen space buffers, so it won’t detect hits “behind” a geometry or out of the screen buffers.

 

 

NB: The HiZ projection model is still in preview. It is currently quite difficult to setup and have many artifacts.

## 

## ReflectionProxyVolumeComponent