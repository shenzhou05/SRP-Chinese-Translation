# Reflection and Refraction

Reflection
Reflection hierarchy
The color contribution for the reflection is computed in multiple steps involving different techniques.

The goal is to get the most accurate color we can than we fallback on less accurate methods.

The reflection hierarchy is:
Screen Space reflection (Opaque only)
Standard / Planar probe reflections
Sky reflection
Screen Space Reflection
The Screen Space Reflection is available only for opaques objects.

It uses the depth and color pyramids from the previous frame.

To configure the Screen Space Reflection add a “Screen Space Reflection” component override in the Volume Component.
Screen Space Reflection Settings
Common Settings

Screen Weight Distance
The screen weight distance is a blending applied when the fetched color is near the boundaries of the screen. (In NDC coordinates)

Example for a weight of 0.1:
The x coordinate will fade as
  X          : 0 -> 0.1 -> 0.9 -> 1.0
  Weight : 0 -> 1.0 -> 1.0 -> 0.0
Projection Model
Projection model to use (Proxy, HiZ)

NB: HiZ is not currently available

Proxy projection model


No additional parameters
HiZ projection model



Ray min level
The minimum mip to use.

The lowest, the most accurate and the most costly.
Ray max level
The maximum mip to use.

The lowest, the most accurate and the most costly.

NB: If this parameter is too high, artifacts may appears
Ray max iterations
Maximum number of iterations before failing.

Use this parameter to cap the cost of this algorithm.
Ray depth success bias
Bias to use when checking when the ray is marching behind an object.

Debugging

Pixel debugging
Click in the view to select a pixel, you will see the queried ray on the screen and the associated information will be displayed in the debug window.

NB: in forward, the debug show the information of the last drawn object and may not be the object you think.
NB: You can press “Home” and mouse your mouse to update the debugged pixel position, So you want interact with the scene while debugging.



The debug information are specific to a projection model and are available once a pixel is debugged.

Proxy projection model

Hit success
Whether the ray successfully hit the proxy and is in front of the camera.
Proxy Shape
The proxy shape used for the raycast
Projection Distance
The distance between the hit and the ray origin
Start position
Ray origin (screen space)
Start linear depth
Linear depth of the ray origin
End linear depth
Linear depth of the hit
End position
Position of the hit (screen space)

Debug modes

Color

Show the color output of the lighting.

RayDirWS

Show the ray direction in world space.

HitDepth

Show the depth of the hit.

HitSuccess

Show whether the ray successfully hit the proxy and the hit point is in front of the camera.

Light green  : Hit success
Light blue    : Hit failed
Other           : No raycast



Reflection Probe
Manual
HDRP Settings
Reflection probes volumes
Proxy volume
Influence volume
The influence volume defines which pixels will use the lighting from this probe.

Blend influence volume
The blend influence volume defines a blending distance from the influence volume and weight the influence of the probe accordingly.

Commonly use to fade the influence between multiple probes.

Blend normal influence volume
A pixel outside of the blend normal influence volume will received a blended influence from the probe.
If this pixel has a normal pointing outwards the capture position, it won’t receive any influence from this probe.

Reflection Probe Inspector
[Insert screenshot]
Primary fields
Edit modes
Influence
Blend
Blend normal
Capture position
Proxy volume
Important notice: The influence volume and the proxy volume must have the same shape type.
Influence volume fields
Capture settings
Additional Settings
Action Toolbar
Cubemap Inspector
[Insert screenshot]

Mip slider
Brightness slider
Mouse rotate
Mouse zoom
Debug Tools
Baking Workflow
Baked
Custom
Realtime
Scripting
Trigger bake
Trigger custom bake
Render a probe

Planar Probe
Manual
HDRP Settings
Planar probes volumes
Proxy volume
Important notice: The influence volume and the proxy volume must have the same shape type.
Influence volumes
See influence volumes of Reflection Probes.

Planar Probe Inspector

Primary fields
Only one workflow is supported for planar probe, so it can’t be modified.
(Realtime, Every Frame, Mirror Camera)
Edit modes


1. Influence volume editing
Edit the bounds of the influence volume.


2. Blend influence volume editing
Edit the bounds of the blend influence volume.
3. Blend normal influence volume editing
Edit the bounds of the blend normal influence volume.
4. Mirror plane position editing
Edit the position of the mirror plane.


 5. Mirror plane rotation editing
Edit the rotation of the mirror plane.


Proxy volume
Choose the proxy volume component (ReflectionProxyVolumeComponent) to use.
If none, an infinite projection will be used.
Influence volume fields
Box shape

Box Size
Size of the box
Box offset
Offset of the center of the box
Influence fade (per axis)
Blend the influence per axis
Influence normal fade (per axis)
Blend the influence normal per axis
Influence face fade (per cube face)
Blend the influence per cube face
Sphere shape

Radius
Radius of the influence
Influence fade
Blend the influence
Influence normal fade
Blend the influence normal

Influence settings fields

Weight
A weight for this probe influence
Multiplier
A multiplier for this probe intensity

Capture settings

Override FOV
Whether to override the capture camera fov
Field of view
Field of view to use when capturing the probe
Render settings
Include the render settings of the capturing camera.
Debug Tools
Baking Workflow
Baked
N/A
Custom
N/A
Realtime
Scripting
Trigger bake
N/A
Trigger custom bake
N/A
Render a probe
FAQ
My planar probe does not reflect anything.
Follow these steps:
Is the influence volume correct?
It should overlap with the reflecting objects.
Is the mirror plane properly placed?
The mirror plane should be placed on your reflecting surface and the normal of the mirror plane must be parallel with the normal of the reflecting surface.
Try editing its position and rotation with the toolbar in the Planar Probe’s inspector.

Refraction
Refraction Hierarchy
(SSRefraction => reflection probe => sky)
Refraction Theory
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
Refraction model
Raycasting & projection
Color sampling
Refraction model
Sphere
We approximate the surface as a sphere with the following parameters:
csphere center=p-n⃗*t*0.5
rsphere radius=t*0.5


Plane
We approximate the surface as a thick plane with the following parameters:
cplane center      =p-n⃗*t*0.5
wplane thickness =t

Common use case
For filled object, you should use a Sphere model with a thickness approximating the size of the object.

For an empty object, you should use a Plane mode with a small thickness.

Projection model
See Appendix - Projection models
Proxy
We approximate the scene by a simple shape and then perform a raycast against this shape the compute the deviated light ray hit.

SUBJECT TO CHANGE IN FUTURE VERSION
Currently the proxy used for the computation is:
The proxy associated to the first environment light found for this pixel (either Reflection probe or Planar probe)
If none, the sky’s proxy will be used (equivalent to an infinite projection)
END
HiZ (Preview)
We perform an accelerated raymarching in the depthbuffer by using a HiZ depth pyramid.
Absorption
When the transmittance color is not white, then the light is attenuated depending on the distance of the light ray within the material.
The greater the distance, the more attenuated the light is.


Transmittance Absorption Distance from 0 (top right) to 6 (bottom left)
Refraction Settings
Material Settings

Refraction model
Define the refraction model to use.
Set to None to disable refraction
SSRay Model
The Projection model to use
Index Of Refraction
The IOR to use for this material.
Refraction Thickness
The thickness to use for the refraction model
Refraction Thickness Multiplier
A multiplier for the thickness.
Transmittance Color
This is the colors that can goes through your transparent. So if you set it to red, the more thick your transparent is, the more green and blue are absorbed.
Transmittance Absorption Distance
This is the approximately the thickness where your object will have the ‘Transmittance Color’ from white light.
Volume Settings
Common Settings

Screen Weight Distance
The distance in NDC to blend the screen space effect.

Use this parameter to blend the screen space effect with the fallback when the sample is near the border of the screen buffer.

HiZ Settings

Ray Min Level
Minimum mip level to use in the HiZ buffer
Ray Max Level
Maximum mip level to use in the HiZ buffer
Ray Max Iterations
Maximum iterations for the HiZ
Ray Depth Success Bias
Bias to use when checking if the ray is behind the current depth buffer value.


Appendix
Projection models
A projection model is used to compute a raycast hit against scene geometry.
Each model is based on a specific resource set and is designed to match a resource budget.
Proxy raycasting
You can define a scene proxy with the ReflectionProxyVolumeComponent.

When performing a raycast, we will raycast against the shape defined in the ReflectionProxyVolumeComponent.

It requires only one depth buffer sample and the projection error is the difference between the proxy volume and the actual scene geometry.

Example of a proxy projection during a reflection:


HiZ raymarching (Preview)
When using HiZ, we raymarch a depth pyramid to calculate the hit.

It is based on screen space buffers, so it won’t detect hits “behind” a geometry or out of the screen buffers.


NB: The HiZ projection model is still in preview. It is currently quite difficult to setup and have many artifacts.

ReflectionProxyVolumeComponent
