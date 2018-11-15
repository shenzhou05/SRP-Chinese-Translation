# High Definition Render Pipeline Glossary


## Lighting
<a name="LuminousFlux"></a>

#### luminous flux:
A measure of the total amount of visible light a light source emits.

![Luminous flux](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/GlossaryLighting1.png)

<a name="LuminousIntensity"></a>

#### luminous intensity:
A measure of visible light as perceived by human eyes. It describes the brightness of a beam of light in a specific direction. The human eye has different sensitivities to light of different wavelengths, so luminous intensity weights each different wavelength contribution by the standard [luminosity function](#LuminosityFunction).

![Luminous intensity](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/GlossaryLighting2.png)

<a name="LuminosityFunction"></a>

#### luminosity function:

A function that describes a wave that represents the human eye’s relative sensitivity to light of different wavelengths. This wave corresponds weight values, between 0 and 1 on the vertical axis, to different wavelengths, on the horizontal axis. For example, the standard luminosity function peaks, with a weight of 1, at a wavelength of 555 nanometers and decreases symmetrically with distance from this value.

<a name="Illuminance"></a>

#### illuminance

A measure of the amount of light ([luminous flux](#LuminousFlux)) falling onto a given area. Differs from luminance because illuminance is a specific measurement of light whereas luminance describes visual perceptions of light.

![](https://github.com/Unity-Technologies/ScriptableRenderPipeline/wiki/Pages/HDRP/Images/GlossaryLighting3.png)





## Light intensity units

<a name="Candela"></a>

#### candela:
The base unit of [luminous intensity](#LuminousIntensity) in the International System of Units. For reference, a common wax candle emits light with a luminous intensity of roughly 1 candela.

<a name="Lumen"></a>

#### lumen:
The unit of [luminous flux](#LuminousFlux). Measures the total quantity of visible light a source emits. A light source emitting 1 [candela](#Candela) of luminous intensity from an area of 1 steradian has a luminous flux of 1 lumen.

<a name="Lux"></a>

#### lux (lumen per square meter):

The unit of [illuminance](#Illuminance). A light source that emits 1 lumen of [luminous flux](#LuminousFlux) onto an area of 1 square meter has an illuminance of 1 lux.

<a name="Luminance"></a>

#### luminance (candela per square meter):

Measures the apparent brightness of light either emitted from a light source, or reflected off a surface, to the human eye. A light source that emits 1 candela of [luminous intensity](#LuminousIntensity) onto an area of 1 square meter has a luminance of 1 candela per square meter.

<a name="EV"></a>

#### exposure value (EV):

A value that represents a combination of a camera's shutter speed and f-number. It is essentially a measurement of exposure such that all combinations of shutter speed and f-number that yield the same level of exposure have the same EV. HDRP Lights can use Ev 100, which is Ev with a 100 International Standards Organisation (ISO) film.

## General Rendering

<a name="Texture atlas"></a>
#### Texture atlas

A texture atlas is a large texture containing several smaller textures packed together. In HD Render Pipeline we use texture atlases for shadow maps and decals.

