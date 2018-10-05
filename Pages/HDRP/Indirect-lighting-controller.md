The **Indirect Lighting Controller** is a Volume component that allows you to globally control the intensity of baked or precomputed indirect lighting.

The **Diffuse lighting intensity** acts as a global multiplier on :

- Baked and Realtime GI lightmaps
- Baked and Realtime GI lightprobes

The **Specular lighting intensity** acts as a global multiplier on :

- Baked, Realtime and Custom Reflection probes

This is useful in situations where your lighting needs to be animated globally. 

### Example scenario

Entering a dark room where all the lights turn on. 

- Setup a Volume with an Indirect lighting controller on it where Diffuse lighting and Specular lighting intensities are set to 0 (so by default all the indirect lighting is dimmed to black)
- When you trigger the lights turning on, animate (through timeline or an animation) the Volume's **Weight** property to transition from 1 to 0 this will progressively interpolate between the values set inside the Volume and the default values (or a volume of lower priority), 
- As a result, you will see the Indirect lighting globally fade in