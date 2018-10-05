Upgrading to HDRP

Conversion Example

The HDRP uses a set of shaders and new lighting units that are incompatible with the Built In Unity rendering pipeline. To upgrade a Project to HDRP you must first convert all of the Materials and Shaders in your project, then you must edit your Light settings accordingly. 

This page demonstrates the HDRP upgrade process using a sample scene containing assets from the Viking Village Asset pack. The scene used in this example can be found at the following Google Drive link.



Setup the High Definition Render Pipeline (HDRP)

First, you must add the HDRP package to your existing Project: 

1. Open the Package Manager window by navigating to Window > Package Manager.
2. Navigate to the All tab and add the “Render-pipelines.high-definition” package.

Next,  create and set up a High Definition Render Pipeline Asset.

1. Navigate to Assets > Create > Rendering > High Definition Render Pipeline Asset.
2. Navigate to Edit > Project Settings > Graphics.
3. Assign the High Definition Render Pipeline asset to the Scriptable Render Pipelines Settings field by clicking the radio button and selecting the asset, or by dragging the asset into the field. 

After installing the HDRP package and assigning the HDRP Asset your scene will not render correctly (see screenshot below). This is because the scene is still using the Built-In Shaders. The below section details upgrading these Built-In Shaders to HDRP. 



Upgrading materials

To upgrade the materials in your scene to HDRP compatible materials, navigate to Edit > Render Pipeline, then select one of the following options: 



- Upgrade Project Materials to High Definition Materials : This option converts all compatible materials in your project to HDRP Materials.
- Upgrade Selected Materials to High Definition Materials : This option only converts Materials that are currently selected in the Project window. 

If your project contains any custom Materials or Shaders then this script will not automatically update them to HDRP. You must convert these Materials and Shaders manually. 

HDRP Lights

The HDRP uses physical Light units to control the intensity of Lights. This means that the arbitrary units used in the Built-In render pipeline will not match the units used in HDRP. 

Directional Light intensities are expressed in Lux ( https://en.wikipedia.org/wiki/Lux ) and other Light intensities are expressed in Lumen ( https://en.wikipedia.org/wiki/Lumen_(unit) ).

So, in the case of our scene, let’s start with the main natural light : the moon. According to Wikipedia, a moonlight with clear night sky has a luminous flux of 1 Lux.

After disabling all other lights (use the Light Explorer), this is what we have.



Yes, we’ve lost the sky. Because HDRP handles the sky differently in volume settings, to allow for example to change sky parameters (among other things) dynamically.

Click in GameObject -> Rendering -> Scene Settings.

This new settings will contain the following components :

- HD Shadow Settings : Stores the max shadow distance and the directional shadow cascade settings.
- Visual Environment : Stores the Sky and Fog type of your scene.
- Procedural Sky : This is a port of the legacy procedural sky and contains the same settings.
- Exponential Fog : The default fog, that does distance and height fog.

Additionally, the gameobject also has a Baking Sky component, that references the Volume’s procedural sky. This component will pass the sky data to the lightmapper and only one should be in the scene at any time.

Here are the settings we will use for the procedural sky : 



About the Exposure and Multiplier values: This sky’s light intensity is expressed as Exposure and Multiplier and to convert to Lux, the best way is to set exposure to 0ev and use the Multiplier as the Lux value. If you look at the wikipedia page, the sky should be at 0.002 Lux, but boosting the value to 0.05 will make it more visible, while still being low enough to be plausible.

You can also enable the light baking at this stage to profit a bit from the light bounces and directional soft shadows.

For the torch lights, because it’s hard to find reference values for this, you can set them around 150 lumen.

You’ll also notice that the light cookie doesn’t work anymore, that’s because HDRP uses standard textures as light cookies, and handles colored cookies. Simply change the cookie texture (named “TorchCookie”) import settings to those :



After a quick light bake, the scene is now looking like this :

 

Some subtle light color tweak later, and we have this in play mode :



The change may not be obvious compared to the legacy screenshot, but that’s because we didn’t use any of the new HDRP specific material features (anisotropy, subsurface scattering, parallax occlusion mapping …) and the original materials were already PBR compliant.

Convert the template scene

An other scene that is interesting to test to convert is the template assets that ships in the “3D with Extra Template”.
Simply create a new project and select this template. You will have this :



Like before, import the HDRP package, and run the converter.

Some of the objects in the scene will have to be modified to act properly:

- Reflection probes will need to be rotated
- The sun light intensity can be set to 100000
- You will need to create a scene settings object and set the sky exposure to 0 and the multiplier to 20000
- The work lamp intensity need to be set to 119000:
- - This is for a 8500 lumen lamp
  - Two lamps
  - And multiply by 7 to compensate for the spot angle and it’s reflector1
  - Correct the light cookie
- Set the emissive intensity of the lightbulb material to 8500.
- Add an Auto-Exposure component to the post processes, with the following settings : 

This will allow to accommodate the high difference in light exposition values (Min and Max), and compensate for the overall high exposure.
- Re-bake the lighting

You should now have a scene similar to this:



Note how the lighting is different from the original one, and from the original HDRP template. Those were made to be good looking but are no realistic, whereas this one with physically correct light values is more plausible: an afternoon direct sun with no clouds in the sky is way brighter than even the best professional construction spotlight.

But the spot is still casting light and shadows on the shadowed side of the wall.

Details

1: On those kind of spot lights, the back of the spot is covered with a reflective surface to reflect all light in the spot direction. In this case we need to compensate the light intensity so the total amount of light inside the light’s cone is the amount of light emitted by the light bulb. The formula is the following:

    Spot Lumen = Bulb Lumen * 2 / ( 1 - cos( half angle ) ) 

What happens when materials are converted

The HDRP material converter will automatically convert Legacy Standards and Unlit materials to HDRP Lit and Unlit.

While the Unlit material conversion is pretty straightforward, converting from Standard to Lit is a bit more tricky. I’ll explain here what is happening behind the scenes, so if something seems wrong to you, you will still be able to do some conversion work manually.
