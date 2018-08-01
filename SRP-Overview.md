From a high level user side SRP can be divided into two parts, the SRP asset, and the SRP instance. Both have an important role to play when crafting a custom render pipeline and when you write a custom pipeline you will need to implement both. 

## SRP Asset
The Asset is a project asset that represents a specific configuration for the pipeline, take for example things like:
* Should shadows be cast
* What shader quality level should be used
* What is the shadow distance
* The default material configuration

Things that users want to have control of be able to save as part of their configuration; basically anything that needs to be serialised. The SRP Asset represents the _type_ of SRP and the settings that are configured.

## SRP Instance
The instance is the class that actually performs the rendering. When unity sees that SRP is enabled it looks at the currently selected asset and asks it to provide a 'rendering instance'. What the asset is required to do in this case is return an instance that contains a 'Render' function. Normally the instance will cache a number of the settings that live in the asset.

The instance represents a know pipeline configuration. From the render call actions can be performed like:
* Clearing the framebuffer
* Performing scene culling
* Rendering sets of objects
* Doing blits from one frame buffer to another
* Rendering shadows
* Applying post process effects

The instance represents the _actual_ rendering that will be performed.