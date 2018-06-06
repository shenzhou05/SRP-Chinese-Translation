## Description

With Unity 2018.1, the graphics team is bringing you all new levels of control and flexibility. Whether you’re a beginner or a pro, we’re empowering you to create amazing projects that look fantastic!

One of the coolest features coming in 2018.1 is [Shader Graph](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph). Freeing you to create a range of shaders; flowing lava, gooey slime mound, beautiful lakes, flashing LEDs, and more!

Designed to work with the [Scriptable Render Pipeline](https://forum.unity.com/threads/feedback-wanted-scriptable-render-pipelines.470095/) (SRP) out of the box, with support for:
- The HD Render Pipeline (Coming soon)
- The Lightweight Render Pipeline
- And the ability to extend the system to export shaders for any custom SRP you write

## What is a Shader Graph?

A [Shader Graph](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph) enables you to build your shaders visually. Instead of hand writing code you create and connect [Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) in a graph network. You can do things like:

- Procedurally alter your surface appearance
- Warp and animate UVs
- Modify the look of your objects using familiar image adjustment operations
- Change your object’s surface based on useful information about it, its world location, normals, distance from camera, etc.
- Expose to the material inspector what you think is important to edit for your shader
- Share node networks between multiple graphs and users by creating subgraphs
- Create your own custom shader graph [Nodes](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) through C# and HLSL
- The graph framework gives instant feedback on the changes, and it’s simple enough that new users can become involved in shader creation.

## How do you create Shader Graphs?

To use [Shader Graph](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph) you must first create a [Shader Graph Asset](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph-Asset). In Unity a [Shader Graph Asset](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph-Asset) appears as a normal shader. To create a [Shader Graph Asset](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph-Asset) you click the create menu in the [Project Window](https://docs.unity3d.com/Manual/ProjectView.html) and select **Shader** from the dropdown. From here you can create either a **PBR** or **Unlit** [Shader Graph Asset](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph-Asset). This will create a [Shader Graph Asset](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph-Asset) in the project. You can double click on the [Shader Graph Asset](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph-Asset) or, with the [Shader Graph Asset](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph-Asset) selected, select the **Open Shader Editor** button in the [Inspector](https://docs.unity3d.com/Manual/UsingTheInspector.html) to bring up the [Shader Graph Window](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph-Window).

## Editing the Shader Graph

When you open the [Shader Graph Window](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph-Window) you start with the [Master Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Master-Node). You connect [Nodes](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) into the [Master Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Master-Node) to create the look of your surface. To learn more about the underlying material models check out the existing Unity [Standard Shader](https://docs.unity3d.com/Manual/shader-StandardShader.html) documentation.

You can quickly edit your surface by changing the default values!

But, you know what’s even more exciting? Adding textures and other complex interactions. To add a node simply right click on the workspace in the [Shader Graph Window](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph-Window) and select **Create Node**.

Each included [Shader Graph](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph) [Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) has a number of input [Ports](https://github.com/Unity-Technologies/ShaderGraph/wiki/Port), we’ve included default values that you can customize however you like!

Adding in a **Texture** (or other assets) is also really easy, just create a [Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) of that [Data Type](https://github.com/Unity-Technologies/ShaderGraph/wiki/Data-Types) and connect it with an [Edge](https://github.com/Unity-Technologies/ShaderGraph/wiki/Edge)!

Your [Shader Graph](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph) shader is just like a normal shader in Unity. Right click create **Material** in the [Project Window](https://docs.unity3d.com/Manual/ProjectView.html) to create a new **Material** you can use on any object in your game. You can create multiple **Materials** from the same shader.

You can expose [Properties](https://github.com/Unity-Technologies/ShaderGraph/wiki/Property-Types) in your shader so they can be overwritten in each **Material** you create from your shader. This is easy. In the shader graph right click on any variable node and select **Convert to property node** or add a new [Property](https://github.com/Unity-Technologies/ShaderGraph/wiki/Property-Types) using the [Blackboard](https://github.com/Unity-Technologies/ShaderGraph/wiki/Blackboard). These exposed [Properties](https://github.com/Unity-Technologies/ShaderGraph/wiki/Property-Types) appear in the **Material** [Inspector](https://docs.unity3d.com/Manual/UsingTheInspector.html) for each **Material** you create from your shader.

To see your new [Shader Graph](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph) changes affect your in game **Materials** click the **Save Asset** button in the [Shader Graph Window](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph-Window)

## How do I get access to the Shader Graph?

It is recommended for users to access the [Shader Graph](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph) via the **Package Manager** or via **Templates**. To use the [Shader Graph](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph) in your project either start a new project using the **Lightweight 3D Template** or download the **Lightweight Render Pileine** via the **Package Manager**. The [Shader Graph](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph) will be downloaded automatically for your use in either of these cases.

### Download from Github

If you wish to download via **Github** we recommend using [Shader Graph](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph) through the [SRP repository](https://github.com/Unity-Technologies/ScriptableRenderPipeline), which has the [Shader Graph](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph) repository setup as a submodule. Otherwise you will not have any [Master Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Master-Node) backends available and thus your shaders will be pink. This also ensure that you get a compatible set of render pipeline and [Shader Graph](https://github.com/Unity-Technologies/ShaderGraph/wiki/Shader-Graph) versions. Otherwise, carry on with the following instructions.

- Create a new project (or use an existing)
- Clone branch `2018.1` into the **Assets** folder of your project, such that the repository is contained in a sub-folder of the **Assets** folder

##  What are the requirements for using Shader Graph

This is a feature for the new [Scriptable Render Pipeline](https://forum.unity.com/threads/feedback-wanted-scriptable-render-pipelines.470095/), available in 2018.1. It will not work out of the box without a SRP.

We won’t be supporting this feature for the legacy renderer.

## I want more tutorials!

More will be coming (including more examples!) over the coming months. We have an end to end shader creation video [Here](https://www.youtube.com/watch?v=pmAHabxNtqU) as a starter point.