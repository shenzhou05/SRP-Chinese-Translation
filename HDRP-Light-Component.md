# The Light Component

 

Use the Light Component to create light sources in your Scene. The Light Component controls the shape, colour, and intensity of the light, along with whether or not the light will cast shadows into your scene and other more advanced settings. 

Light Components can be configured using the Light Component inspector window. 

![img](https://lh3.googleusercontent.com/SqF_UcAktbK0eUUi9gmmpGRdXiKVpyQk8QnCkIz2me-UHu5YYcJESUvF72iS-7xDYXXOUuRf4WGDsLI42HWN-5XFH-X3uoXRJZbOtiEcxgzJcFR1INPkI3u9wlobBu6c_5yhNPMO)

## Features :

Use the Features section to enable or disable shadows and additional settings for this light. 

- **Shadows** : Tick this box to make this Light cast Shadows into your scene. Ticking this box makes the Shadows section appear in the Light Component Inspector window. Use the settings in the Shadows section to configure the Shadows cast by this light. 
- **Show additional settings** :  Tick this box to display additional settings in the Light Component Inspector window.  The default settings are suitable for most use-cases, but additional settings can be used to fine-tune your Light component if you need to achieve a specific look or light behaviour.  If you are writing your own Light system using SRP then you can expose your own light settings here. 

## Shape : 

Use the Shape section to change the shape of your Light. 

* **Type**: Use this dropdown to select the shape of your Light
  * **Directional light** : Directional lights are used to create effects such as sunlight in your scenes. Behaving in many ways like the sun, directional lights can be thought of as distant light sources which exist infinitely far away. A directional light does not have any identifiable source position and so the light object can be placed anywhere in the scene. All objects in the scene are illuminated as if the light is always from the same direction. The distance of the light from the target object is not defined and so the light does not diminish.
  * **Point light** : A point light is located at a point in space and sends light out in all directions equally. The direction of light hitting a surface is the line from the point of contact back to the center of the light object. The intensity diminishes with distance from the light, reaching zero at a specified range. Light intensity is inversely proportional to the square of the distance from the source. This is known as ‘inverse square law’ and is similar to how light behaves in the real world.
  * **Rectangle** : A Rectangle Light is defined by a rectangle in space. Light is emitted in all directions uniformly across their surface area, but only from the surface of the rectangle. 
  * **Line** : A Line Light is defined by a line in space. Light is emitted in all directions uniformly along the line. 
  * **Spot** : Like a point light, a spot Light has a specified location and range over which the light falls off. However, the spot Light’s constrained to an angle, resulting in a cone-shaped region of illumination. The center of the cone points in the forward (Z) direction of the light object. Light also diminishes at the edges of the Spot Light’s cone. Widening the angle increases the width of the cone and with it increases the size of this fade, known as the ‘penumbra’.

    * Cone shape (Spot light only) : use Cone Shape adjust the shape of the Spot Light. Possible values are: Cone, Pyramid, and Box.

    * Spot Angle (Spot light only) : The Spot Angle setting defines the angle (in degrees) at the base of a Spot Light’s cone.

    * Inner Percent (Spot light only) : Determines where the attenuation between the inner cone and the outer cone starts. Higher values will cause the light at the edges of the Spot to fade out, while lower values will stop the light from fading at the edges. 
    * ![Inner Spot percent example](https://lh5.googleusercontent.com/ijE6NOhZ8MQ5wwKnLJGUxStxF-nf6bRUic0L94krjgpbfQ19PdZHgFGcpBXqIe4Ax7XwyoEgipdf8f_7DcOhMzZzmZMDZLEJxvvHUA29PkqzXTLlXG8ymZ7keueRYluelzwn80lc)
     * Aspect ratio (pyramid spot light only) : Use the Aspect Ratio setting to adjust the shape of a Pyramid spot light and create rectangular spot lights. Lower values cause the light to be longer as seen from the point of origin, while higher values make the light wider.

    * Size X / Size Y (box spot light / rectangle light only) : Use the Size X and Y settings to adjust the size of the box or rectangle Light. For Box Spot Lights, no Light will shine outside of the dimensions set in Size X and Y. For Rectangle lights, this setting dictates the size of the emission rectangle. 

    * Length (line light only) : This setting adjusts the length of a Line Light. Light will be emitted along the full length of the Line Light. 

    * Max smoothness (Spot and Point only) : Use Max smoothness to change the aspect of the specular highlight in order to mimic an area light. This allows you to avoid very sharp specular highlights not matching the shape of the light source.


**Light**: 

Use the Light section to adjust the way your Light Component emits light into your scene.

* **Use color temperature mode** : Tick this box to enable color temperature mode for this Light. Use color temperature mode to adjust the colour of your light based on a red to blue temperature scale. The colour is then automatically multiplied by the color selected in the Color field. 

* **Color** : Use the color picker to select the colour of the emitted light. 

* **Intensity** : Intensity of the light expressed in *unit*. The further the light travels from its source, the more it diminishes.

  * Directional light : unit = lux

  * Point / spot /rectangle / line light = lumens

* **Indirect Multiplier** : intensity multiplier applied on the indirect lighting computed through baked global illumination and realtime global illumination. A value of 1 mimics a realistic light behavior. A value of 0 disables bounced lighting for this light.

* **Range** : distance from the light source within which lighting will be evaluated. By default, a range attenuation is applied near the range distance so that the border fades softly.

* **Mode** : Specify the [Light Mode](https://docs.unity3d.com/Manual/LightModes.html) used to determine if and how a light is “baked”. Possible modes are Realtime, Mixed and Baked. See documentation on [Realtime Lighting](https://docs.unity3d.com/Manual/LightMode-Realtime.html), [Mixed Lighting](https://docs.unity3d.com/Manual/LightMode-Mixed.html), and [Baked Lighting](https://docs.unity3d.com/Manual/LightMode-Baked.html) for more detailed information.

* **Cookie** : Specify a RGB Texture that the light will project (for example, to create silhouettes, or patterned illumination for the Light). Texture shapes should be Texture 2D for Spot Lights and Texture Cube for point lights. The rapping modes clamp, repeat, and per axis are supported, but only affect directional lights. 

Caution: Cookie texture need to be imported as Default texture type. HDRP support RGB cookie unlike Buitin Unity which support only grey texture imported with Cookie Texture type

* **Size X / Size Y** (Directional light only) : Use this to define the size of the cookie texture projection.

  **Additional settings :**

  * **Affect Diffuse** : Tick this box to enable diffuse lighting for this light 

  * **Affect Specular** : Tick this box to enable specular lighting for this light Fade Distance : Use this to set the distance at which the light will fade out.

  * **Dimmer** : Use this to dim the light without affecting the intensity. This parameter can also be modified using timeline, scripting or animation and allows you to fade the light in and out without having to store its original intensity.

  * **Apply range attenuation** (not available on directional light) :Tick this box to enable range fade on the light. This is useful when the range limit is not visible on screen (typically in indoor scenarios or streetlamps shining onto the ground.

**Shadows** :

Use the Shadow section to adjust the way your Light Component casts shadows into your scene.

* **Resolution** :Use this to sets the resolution of the shadows cast by this light

* **View bias scale** : multiplier applied to shadow bias depending on the distance to the light

* **Near Plane** :Use this to set the distance from the light at which objects start casting shadows

* **Baked shadow radius** (mixed and baked lights only) : Values higher than 0 make the light behave as a sphere whose radius is this value for the lighting bake.  High values result in shadows that soften with distance from the shadow caster.

  **Additional Settings :** 

  * **Fade Distance** : Use this to set the distance between the camera and the light at which shadows will fade out.
  * **Dimmer** :Use this to dim the shadows cast by this light. This parameter can be also be modified through scripting, timeline or animation.
  * **View Bias** : Use this to set the minimum shadow bias in view space applied to the shadow projection
  * **Normal Bias** : Use this to set the shadow bias applied along the surface’s norma. 
  * **Edge leak fixup** : Tick this box to apply a fix that helps prevent light leaking at the edge of shadows cast by this light.
  * **Edge Tolerance normal** : Tick this box to use the edge leak fix in normal mode. Untick to use it in view mode.
  * **Edge Tolerance** :Use this to set the threshold used to determine whether to apply or not edge leak fixup.
  * **Contact shadows** : Tick this box to enable contact shadows for this light. Only one visible light on screen can use contact shadows.

 