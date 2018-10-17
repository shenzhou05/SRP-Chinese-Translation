Use the Light Component to create Light sources in your Scene. The Light Component controls the shape, color, and intensity of the Light. It also controls whether or not the Light casts shadows into your scene, as well as more advanced settings. 
​    
## Creating Lights

There are two ways to add Lights to your scene. You can create a new Light GameObject, or you can add a Light Component to an existing GameObject. 
To create a new Light Gameobject:   

1. Navigate to GameObject > Light. Then select the light type you want to add. 
  
Your new light is then automatically added to your scene, centered on your current view of the Scene in the Scene window. 
To add a Light Component to an existing GameObject:

1. Click __Add Component__ in the Inspector, 
2. Navigate to Rendering and click Light. This creates a new Light source attached to the currently selected GameObject
3. You can also search for “Light” in the __Add Component__ window, then click Light to add the Light Component. 
  
## Configuring Lights

Select a Light GameObject and use the Light Component Inspector window to configure that Light Component. 

The options presented in this window change depending on the type of light you have selected and if the Enable Shadows or Show Additional Settings checkboxes are ticked. 
![img](https://lh5.googleusercontent.com/Ug30tDUAgNu11kkEl2_f7U5XJGVoDs8rSMU7i0x1yy1eQjWu50M5FBFt2CtRCPqTzh-dhpmTwVpuDMGCQP4lIXZqXcLRolGY86LYEnJeB1sUt8nOdEEtq9-Iyw9k4wuF361C24ut)
_The Light Inspector window for a Directional Light with Enable Shadows and Show Additional Settings selected._
​    

## Features :

Use the Features section to enable or disable shadows and additional settings for this Light. 
​    
- **Shadows** : Check this box to make this Light cast Shadows into your scene. Checking this box makes the Shadows section appear in the Light Component Inspector window. To configure the Shadows cast by this light, use the settings in the Shadows section.
  ​    - **Show Additional Settings** :  Check this box to display additional settings in the Light Component Inspector window.  The default settings are suitable for most use-cases, but you can use the additional settings to fine-tune your Light Component for a specific look or Light behaviour.  If you are writing your own Light system using SRP, then you can expose your own Light settings here. 
## Shape : 

Use the Shape section to change the shape of your Light. 

**Type**: Use this dropdown to select the shape of your Light
​        

- **Directional Light** : Directional Lights are used to create effects similar to sunlight in your scenes. Like sunlight, directional lights are distant light sources that exist infinitely far away. A directional Light does not have any identifiable source position, and you can place the Light object anywhere in the scene. All objects in the scene are illuminated as if the Light always comes from the same direction. The distance between the Light and the target object is not defined, so the Light does not diminish with distance.

- **Point Light** : A point Light is located at a point in space. It sends Light out in all directions equally. The direction of Light hitting a surface is the line from the point of contact back to the center of the Light object. The Light intensity diminishes the further away it is from the Light, and it reaches zero at a the range specified in the Range field. Light intensity is inversely proportional to the square of the distance from the source. This is known as ‘inverse square law’, and is similar to how Light behaves in the real world.

- **Rectangle** : A Rectangle Light is defined by a rectangle in space. From the surface of the rectangle, Light shines in all directions uniformly across their surface area.
  ​      
- **Line** : A Line Light is defined by a line in space. Light shines in all directions equally along the line. 

- **Spot** : Like a point Light, a spot Light has a specified location and range over which the Light diminishes. However, the emitted light is constrained to an angle, which results in a cone-shaped region of illumination. The center of the cone points in the forward (Z) direction of the Light object. Light also diminishes at the edges of the Spot Light’s cone. Widen the angle to increase the width of the cone.

  - **Cone shape** (Spot Light only) : use Cone Shape to adjust the shape of the Spot Light. Possible values are: Cone, Pyramid, and Box.

  - **Spot Angle** (Spot Light only) : The Spot Angle setting defines the angle in degrees at the base of a Spot Light’s cone.

  - **Inner Percent** (Spot Light only) : The inner percent value determines where the attenuation between the inner cone and the outer cone starts. Higher values cause the Light at the edges of the Spot to fade out. Lower values stop the Light from fading at the edges. 

  - **Aspect ratio** (pyramid Spot Light only) : Use the Aspect Ratio setting to adjust the shape of a Pyramid Spot Light, and create rectangular Spot Lights. The Light will be square if Aspect ratio is set to 1. Values lower than 1 will make the Light  wider as seen from the point of origin, values higher than 1 will make the Light longer.

  - **Size X / Size Y** (box Spot Light / rectangle Light only) : Use the Size X and Y settings to adjust the size of the box or rectangle Light. For box Spot Lights, no Light shines outside of the dimensions set in Size X and Y. For Rectangle Lights.![img](https://lh5.googleusercontent.com/ijE6NOhZ8MQ5wwKnLJGUxStxF-nf6bRUic0L94krjgpbfQ19PdZHgFGcpBXqIe4Ax7XwyoEgipdf8f_7DcOhMzZzmZMDZLEJxvvHUA29PkqzXTLlXG8ymZ7keueRYluelzwn80lc)
  - **Max smoothness** (Spot and Point LIghts only) : Use Max smoothness to change the the specular highlight in order to mimic a rectangle light. This allows you to avoid very sharp specular highlights that do not match the shape of the Light source.

- **Length** (line Light only) : This setting adjusts the length of a Line Light. Light shines along the full length of the Line Light.
- **Range** (Not available on Directional Lights) : Use the Range value to control how far light shines from the center of the object. 
  ​      
## Light: 

Use the Light section to adjust the way your Light Component shines Light into your scene.
​        
- **Use color temperature mode** : Check this box to enable color temperature mode for this Light. Color temperature mode adjusts the color of your Light based on a red-to-blue kelvin temperature scale. This color is then multiplied by the color specified in the color field. When this box is unchecked, only the color field is displayed in the Inspector and used, without the temperature.

- **Color** : Use the color picker to select the color of the Light using the colour picker, RBG or HSV values. 

- **Intensity** : Use the Intensity value to change the intensity of the Light. Intensity is expressed in the units specified below. The further the Light travels from its source, the more it diminishes. Lower values cause Light to diminish closer to the source. Higher values cause Light to diminish further away from the source. 

  - Directional Light : unit = lux
    
  - Point / Spot / Rectangle / Line Light = lumens

- **Indirect Multiplier** : Use the Indirect Multiplier value to change the intensity of [indirect ](https://docs.unity3d.com/Manual/LightModes-TechnicalInformation.html)Light in your scene. A value of 1 mimics realistic light behaviour. A value of 0 disables indirect lighting for this light. If both Realtime and Baked Global Illumination are disabled, the Indirect Multiplier has no effect. 

- **Mode** : Specify the [Light Mode](https://docs.unity3d.com/Manual/LightModes.html) used to determine if and how a Light is baked. Possible modes are Realtime, Mixed and Baked. See documentation on [Realtime Lighting](https://docs.unity3d.com/Manual/LightMode-Realtime.html), [Mixed Lighting](https://docs.unity3d.com/Manual/LightMode-Mixed.html), and [Baked Lighting](https://docs.unity3d.com/Manual/LightMode-Baked.html) for more detailed information.

- **Cookie** : Specify a RGB Texture that the Light projects. For example, to create silhouettes or patterned illumination for the Light. Texture shapes should be 2D for Spot Lights and Cube for Point Lights. Cookie textures must be imported as the default texture type. 

- **Size X / Size Y** (Directional Light only) : Use this to define the size of the projected cookie texture in pixels.
  ​      
**Additional settings** :
​        
- **Light Layer**: Use this to chose the Light Layers that this Light should affect. 
- **Affect Diffuse** : Check this box to enable diffuse Lighting for this Light. 
- **Affect Specular** : Check this box to enable specular Lighting for this Light. 
- **Fade Distance**: Use this to set the distance in meters between the light source and the camera at which the Light begins to fade out. 
- **Dimmer** : Use this to dim the Light without affecting the intensity. You can also modify the dimming parameter via Timeline, scripting or animation. The parameter  lets you to fade the Light in and out without having to store its original intensity.
- **Volumetric Dimmer** : Use this to adjust the intensity of scattered volumetric lighting for this Light. 
- **Apply range attenuation** (not available on Directional Lights): Uncheck this box to make this light shine uniformly across its range. This stops light from fading around the edges. This setting is useful when the range limit is not visible on screen, and you do not want the edges of your Light to fade out. 
- **Display Emissive Mesh**: Tick this checkbox to make Unity automatically generate an emissive mesh using the size, colour and intensity of this Light. The mesh is automatically added to the GameObject the Light component is attached to. 
  ​      
## Shadows :

Use the Shadows section to adjust the Shadows cast by this light.
​        
- **Resolution** : Use this to set the resolution in pixels of the shadow maps used by this light. A higher resolution will increase the fidelity of shadows at the cost of GPU performance and memory usage.
- **View bias scale** : Use this slider to adjust how much the [View Bias](https://docs.unity3d.com/Manual/ShadowOverview.html#LightBias) scales with distance for this light. Surfaces directly illuminated by a Light can sometimes appear to be partly in shadow, or parts of the surface can be incorrectly illuminated due to low-resolution Shadow maps or Shadow Filtering. If the Shadows Cast by this Light appear incorrectly, use the slider to adjust this value until they are correct.
- **Near Plane** : Use this to set the distance from the Light where objects start casting shadows.
- **Baked** shadow radius (Mixed and Baked Lights only) : Values higher than 0 make the Light behave as a sphere whose radius is this value for the Lighting bake.  High values result in shadows that soften with distance from the shadow caster.
- **Non Lightmapped Only** (Mixed Lights only) : Ticking this checkbox forces this Light to use the baked Shadowmask for static objects, and only render dynamic shadows for dynamic objects. 
  ​      
**Additional Settings** : 
​        
- **Fade Distance** : Edit the Fade Distance value to set the distance in units between the camera and the Light where shadows fade out.
- **Dimmer** : Use this to dim the shadows cast by this Light. You can also modify this parameter through Timeline, scripting or animation. 
- **View Bias** : Use this to set the minimum [View Bias](https://docs.unity3d.com/Manual/ShadowOverview.html#LightBias) for this light. See documentation on [Shadows ](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Shadows)for more information about View Bias. 
- **Normal Bias** : Use this to control the amount of normal [bias](https://docs.unity3d.com/Manual/ShadowOverview.html#LightBias) applied along the normal of the illuminated surface. 
- **Edge leak fixup** : Check this box to prevent Light leaking at the edge of shadows cast by this Light.
  - **Edge Tolerance normal** : Check this box to use the edge leak fix in normal mode. Uncheck this box to use the edge leak fix in view mode.
  - **Edge Tolerance** : Use this to set the threshold that determines whether to apply the edge leak fixup.
