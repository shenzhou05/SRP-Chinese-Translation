The core or SRP is a collection of API's that push many of the rendering internals and configuration out into user land. This give you the power to configure exactly how you want rendering to work in your project.

The SRP API offers a new interface to many familiar Unity constructs. You will still be using:
* Lights
* Materials
* Cameras
* Command Buffers

But the _way_ you interact with Unity is different. For performance reasons when writing a custom SRP you generally work with groups of renderers, not individual items.