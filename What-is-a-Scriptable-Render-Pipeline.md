If a Render Pipeline is a number of steps that are performed to perform rendering onto the screen, a Scriptable Render Pipeline is a pipeline that can be controlled from Unity scripting code to perform rendering in a user defined way.

## The Problem
Traditionally with Unity we have provided a number of built in pipelines that can be used, some better for mobile / vr (the forward renderer), and some fore more high end games (the deferred renderer). These out of the box rendering solutions have been designed to be very general and black box, but that comes with a downsides

* They only do what they are designed to do
* They are designed to be general, which means that because they need to do everything they are masters at nothing
* They are not very configurable (black box with injection points)
* Extension and modification is prone to error (small internal changes can have big outward ramifications)
* Many bugs can't be fixed (as this changes behaviour which can break projects).

## The Solution
The SRP API is designed to resolve the problems described above. What it does it change rendering from being a black-box inbuilt concept to being a user controlled per project scriptable concept. Using the SRP api it's possible to have fine grain customisable control of how rendering is performed, form the low level to the high level. 