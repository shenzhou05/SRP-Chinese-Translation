# Atmospheric Scattering

Fog is the effect of overlaying a color onto objects dependant on the distance from the camera. This is used to simulate fog or mist in outdoor environments and is also typically used to hide clipping of objects when a camera’s far clip plane has been moved forward for performance.

In HDRP, users can choose between different kind of fogs, [Linear](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Linear-Fog), [Exponential](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Exponential-Fog) and [Volumetric](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/HDRP-Volumetric-Fog) fog. All types of materials (lit or unlit) will react correctly to the fog. Depending on the type of fog, density will evolve differently with respect to distance from camera and world space height.

Instead of using a constant color, Linear and Exponential fog can choose to use the background sky as a source for color. In this case, the color will be sampled from different mip maps of the cubemap generated from the current sky settings. Chosen mip will vary linearly between the blurriest one to the highest resolution one depending on the distance from camera and the “Mip Fog” parameters. Users can also choose to limit the resolution of the higher mip used. This adds a sort of "volumetric" effect to the fog for much cheaper than actual volumetric fog.

## Creating Volumetric Fog

- Be sure to enable "Support Volumetrics" and optionally enable "Increase resolution of volumetrics" in your HDRP asset:
 ![img](https://lh3.googleusercontent.com/LKkNaNVzpMWN_WJ-svF50Z_xM3bac7oMzDACJi4qQwTQ0zycmldwCYS_VvGeLbEf8CG_sLa4InW6NFCf0stRZ3elZLCg2MGXfOBl_TSiM3y0jvZIT8QIOYsJcBjXmaE4kh5dPuUS)
- 
- In the Volume Settings of your scene, add a "Volumetric Fog" and a "Volumetric Lighting Controller" component.
- Change the "Fog Type" value of the "Visual Environment" to "Volumetric".
 ![img](https://lh6.googleusercontent.com/zcp6qNg4Yn6EAcreqZJ3f_gQ_Dp6z11vMX3KQR74Z44C9yroo6SaLJN_kptUbeeZN67KqAmfA_ZbtjsB4RQl3DezomflPMaQmnpJhaX5lyGjMbXakGwJTj-J74tQhsEk-l96eVWa)
- You should already be able to see the volumetric fog in the scene and game view.
- If it doesn't show up in the scene view, check that the fog toggle is enabled in the scene view :
 ![img](https://lh4.googleusercontent.com/caVxRGTymngkUu73r3NApfD1i4ZPCQpAeJzRVf6we-Sd1Ko3MmTI7w76PxUxVdK3C0HZIeL-4CVehXdwpw3JgbphTdqhMjhBehgLDzrUr6GB6BDeWADL-55az1wdlD_6uudaRKcA)

- Note that by default, the fog density is very low. This is set by the "Mean Free Path" parameter : the lower the parameter, the higher is the density of the fog.
- Now you can add a density volume object in your scene to control the fog density locally :
![upload_2018-7-18_13-30-7.png](https://lh3.googleusercontent.com/xraINdZZDp0y1j5ZJfiWtzEtFuQX9trcc-A1XdyZ6Juzz4GjSlreeVWNvZtOSxgNMC53Hz2_I-J6Pe7y6obSwJfSTyWAdiic3CDf9F48X-iA24cLudg2AYv8wYOtnmFb-7qh6Ei0)         

- Here I added a blue fog with a point light inside in the scene :

![upload_2018-7-18_13-35-8.png](https://lh5.googleusercontent.com/IaUuFvUnSZ1G6fmtJdvv0RtUyHP5uQyqiyT9GsctIp_bPM0WoSLNR8DKhPMAaAZy0eFzUA_Zz-PTkPsqk6wADdHRnmJCLRkoGuhIRIL2dsmQlIoTABOo8g49zwNwkQKj1WYBF8Ti)         

Now for the density texture :

I modified the example script of texture 3D so that the generated texture can be use in a density volume. Here is my code :

```
Code (CSharp):

1. using System.Collections;
2. using System.Collections.Generic;
3. using UnityEngine;
4. using UnityEngine.Experimental.Rendering.HDPipeline;
5. using UnityEngine.Experimental.Rendering;
6.  
7. [RequireComponent([typeof](http://www.google.com/search?q=typeof+msdn.microsoft.com)(DensityVolume))]
8. public class Texture3DToDensityVolume : MonoBehaviour
9. {
10.  
11.     Texture3D texture;
12.  
13.     void Start ()
14.     {
15.         // The curent density volume texture size is hard coded to be 32
16.         texture = CreateTexture3D (32);
17.  
18.         DensityVolume densityVolume = GetComponent<DensityVolume>();
19.         densityVolume.parameters.volumeMask = texture;
20.     }
21.  
22.     Texture3D CreateTexture3D (int size)
23.     {
24.         Color[] colorArray =[ new](http://www.google.com/search?q=new+msdn.microsoft.com) Color[size * size * size];
25.         texture =[ new](http://www.google.com/search?q=new+msdn.microsoft.com) Texture3D (size, size, size, TextureFormat.Alpha8, true);
26.         for (int x = 0; x < size; x++) {
27.             for (int y = 0; y < size; y++) {
28.                 for (int z = 0; z < size; z++) {
29.                     // Calculate the radius
30.                     float f =Mathf.Sqrt(
31.                         Mathf.Pow( 2f * ( x - 0.5f*size ) / size, 2 ) +
32.                         Mathf.Pow( 2f * ( y - 0.5f*size ) / size, 2 ) +
33.                         Mathf.Pow( 2f * ( z - 0.5f*size ) / size, 2 )
34.                         );
35.                     // Fill pixels of radius <=1 with alpha = 1
36.                     f = (f <= 1f )? 1f : 0f;
37.                     Color c =[ new](http://www.google.com/search?q=new+msdn.microsoft.com) Color (1.0f, 1.0f, 1.0f, f);
38.                     colorArray[x + (y * size) + (z * size * size)] = c;
39.                 }
40.             }
41.         }
42.         texture.SetPixels (colorArray);
43.         texture.Apply ();
44.         return texture;
45.     }
46.        
47. }
```

As you can see, the texture format used has to be Alpha8, as we only need one channel to store the density multiplier.

Alternatively, you can create a static density 3D texture.

For the example, I used this texture, authored in photoshop :

​         ![upload_2018-7-18_14-22-29.png](https://lh4.googleusercontent.com/t1uhoRpOSdbnqm22Uu17dU0WPataxzGpVn6lzFS9g3hJ1FrhL3rZqmK9Eae5c4ejyBSprPjjRV7F4b-7PpTjaDni4MkazKClcIet2qp7UoyZlnW7k7r8DcqOPeRmaT4x5JIuwMo0)         

It contains 32 slices of 32x32 pixels.

Import it using these settings :

​         ![upload_2018-7-18_14-23-10.png](https://lh4.googleusercontent.com/Mx5NPjDYJitByhWT9IJFXT94Zg--KSKaAjuylVO9OgIK3PuVIdhZuTxs475Ozpipf7fd5dVOlbBNFwIMqztwUC5L2L_vp82OpKNG-HTZBQthEsCkoyfbKQ9B3WYcwENJfqjLx58o)         

Now, open the 3D texture creation tool:

​         ![upload_2018-7-18_14-23-46.png](https://lh5.googleusercontent.com/98hgTu0h8aGNNZZAtIVCTFUgiqbULEscKwzUZFd6daDG3saGpjGNn6GvH_AyeG0UmfvwPrsNg3MHPHMhbl17a1mfiWjP2G8043cKoaDJFFoloI9DX65Kob_Zk4yywgBbVSyMVRXC)         

Drop the texture in the texture field and hit "Generate 3D Texture":

![img](https://lh3.googleusercontent.com/QXfmIiZ-bDO-YotGLMt2AVbJSWbeQQchJFzcyhTURKn7h3f7LBmthxe7IOpuigjdxWGwgZLQTy3Wz2GExlCAyjsdJ7iMXIoxsCWtTSYDJ-_vdOw7q-iMq6z-oaE0YhfHJurEQ18B)

The newly created 3D texture is saved in the same folder as the original one, and can be used in the density volume settings.

This one will render rings like this :

![img](https://lh4.googleusercontent.com/m1bV3ITdIenGpHSO2opgo463Y73aK9gwP_KJpw-RgvfXpipd6hQqi_-obpoO0DmYJVIF6RK-x-OhUsglREs8IZIUmTnIrBhBDtVmG1Vo-mV7X4D-BxFTKmZufs4_hQpZ0yHfQB7e)

![:)](https://lh5.googleusercontent.com/XG1-xPDcRcXoa1YYwnaNmGG4nei52zgwJCBaXQ4l78sACDxKHWByJ-6cJfAjK9nmGa8TbYN4Hyo_XKB08V2orunyC58VGyZv1RHmKfQbGHttrd9qzkpG6cSt2gVcgZNeuFdGSVej)