# Systems, Contexts and Blocks

The visual effects system relies on a modular flow design where processing is described through states. Systems are composed by chaining states which contains dedicated behavior. Each state type has its own specific properties and using a behavior block in one state or another can be used to achieve different results.

## Systems

Systems are generally composed of a **top-to-bottom chain of contexts** that follows this order : 

![](C:\Unity\VFX Help\img\system-contexts.png)

## Contexts

### Event

Event contexts are flow inputs that will turn on and off the spawn of particles, These contexts are simple and only contain a string that will define their names. The `OnPlay` and `OnStop` events are dedicated event names that correspond to the `Play()` and `Stop()` methods of the component, which can be considered as an **intent of start spawning particles**, and another intent of **stop spawning particles**.

Events can also have any custom name defined as a string, and thus can be invoked by the `SendEvent()` method of the Visual Effects component.

![](C:\Unity\VFX Help\img\events.PNG)

### Spawn

Spawn and events contexts are triggered by **SpawnEvent** data types and can be chained to synchronize themselves. **SpawnEvent**s can be considered as messages containing a **spawn order** with a **spawn count** , and a **state payload**.

Spawn Contexts have two inputs : **Start** and **Stop**. These are implicitly bound to the `OnPlay` and `OnStop` events, which means that the spawning machine will start spawning when some SpawnEvent hits the start flow input, and shutdown when another SpawnEvent hits the stop flow Input.

![](C:\Unity\VFX Help\img\implicit-events-spawner.PNG)

Every time the Start input is hit by a SpawnEvent, the Spawn context internal time resets to zero, and spawn resets. So if a Single burst happens at T=0s it will be triggered every frame a spawn event hits the start input.

#### Spawn and Event State

Event state is conveyed through the SpawnEvent flow, from one Spawn context to another, and overwritten into the spawn context every time a SpawnEvent hits the start flow input. 

> **Special Case :** If two SpawnEvents hits the input at the same frame, only the last event hitting the spawn context will store its state palyoad into it.
>
> Also, the spawn context reset will happen twice but the execution only once, by default. As the time will reset to zero once (with the first event), then another time (with the second event), then spawn blocks will be executed.
>
> If you need to accumulate spawn orders happening at the same frame, see the [Custom Spawners]() section.

### Initialize

Initialize contexts are the makers of new particles and are executed when a SpawnEvent hits the input. 

#### Behavior

The context will create an amount of particles equal to the **spawnCount** of the SpawnEvent data payload. For each new particle, the context blocks will be executed, then the particles inserted into the simulation.

#### Properties/Settings

* (*Setting*) **Capacity** : the allocation count for particles, It should reflect the expected amount of particles you need for this system. If initialize does not find any room for all new particles in the simulation pool, some or all new particles could be discarded.
* **Bounds** : The bounding box corresponding to the extents of the system. As this is a property, It can be computed using operators.

### Update

Update contexts updates particles attributes every frame and update their state along time.

#### Behavior

Update context processes every particle in the simulation if it is alive, every frame. It can also handle automatically some tasks. such as particle aging and reaping, and the integration of the velocity to the position. These automatic settings can be disabled if you need to perform this tasks in a more custom way.

Update contexts can be skipped if no update is necessary. Connecting an initialize to an output will perform a update-less simulation with particles initialized at start and rendered following their initial state.

#### Properties/Settings

* (*Setting*) **Integration** : (Euler or None) If this option is set to Euler, the positions will be integrated from velocity every frame following the euler model.
* (*Setting*) **Age Particles** : if Age attribute is set, every particle will age accordingly to the current deltaTime
* (*Setting*) **Reap Particles** : if Age and Lifetime attribute are set, every particle which age goes beyond Lifetime will be killed.

### Output

Output contexts are executed every frame and will give shape to the simulated particles for every living particle. Many output contexts exist and have their own specificities.

#### Behavior

Output contexts take, every frame, the simulation data and will render it according to the context configuration. Also, blocks can be used to perform computation before rendering. However, **the output context does not modify the simulated data**, so block operations made in this context can be considered as pre-render operations. 

An Initialize or update block **can be connected to multiple outputs at once**. The simulation data will be shared across these output contexts.

#### Settings

Depending on the output context you use, settings are subject to change. See the Output context reference for more information.

## Blocks

