What is a Render Pipeline
“Render Pipeline” is an umbrella term for a number of techniques used to get objects onto the screen. It encompasses, at a very high level:
* Culling
* Rendering Objects
* Post processing

In addition to these high level concepts each responsibility can be broken down further depending on how you want to execute them. For example rendering objects could be performed using:
* Multi-pass rendering - one pass per object per light
* Single-pass - one pass per object
* Deferred - Render surface properties to a g-buffer, perform screen space lighting

When writing a custom SRP, these are the kind of decisions that you need to make. Each technique has a number of trade offs that you should consider.