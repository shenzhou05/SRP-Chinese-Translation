## Description

The **Shader Graph Window** contains the workspace for creating shaders using the **Shader Graph** system. To open the **Shader Graph Window** you must first create a [Shader Graph Asset](https://github.com/Unity-Technologies/ShaderGraph/wiki/Home). For more information see the [Getting Started](https://github.com/Unity-Technologies/ShaderGraph/wiki/Getting-Started) section.

The **Shader Graph** window contains various individual elements such as the [Blackboard](https://github.com/Unity-Technologies/ShaderGraph/wiki/Blackboard) and [Master Preview](https://github.com/Unity-Technologies/ShaderGraph/wiki/Master-Preview). These elements can be moved inside the workspace. They will automatically anchor to the nearest corner when scaling the **Shader Graph Window**.

## Title Bar

The title bar at the top of the **Shader Graph Window** contains actions that can be performed on the **Graph**.

| Item        | Description |
|:------------|:------------|
| Save Asset | Saves the graph to update the [Shader Graph Asset](https://github.com/Unity-Technologies/ShaderGraph/wiki/Home) |
| Show In Project | Hightlights the [Shader Graph Asset](https://github.com/Unity-Technologies/ShaderGraph/wiki/Home) in the [Project Window](https://docs.unity3d.com/Manual/ProjectView.html) |

## Workspace

The workspace is where you create [Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) networks. 
You can navigate the workspace by holding Alt and left mouse button to pan and zoom with the scroll wheel.

You can hold left mouse button and drag to select multiple [Nodes](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) with a marquee. There are also various shortcut keys to use for better workflow.

| Hotkey      | Windows     | OSX         | Description |
|:------------|:------------|:------------|:------------|
| Cut | Ctrl + X | Command + X | Cuts selected [Nodes](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) to the clipboard
| Copy | Ctrl + C | Command + C | Copies selected [Nodes](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) to the clipboard
| Paste | Ctrl + V | Command + V | Pastes [Nodes](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) in the clipboard
| Focus | F | F | Focus the workspace on all or selected [Nodes](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node)
| Create Node | Spacebar | Spacebar | Opens the [Create Node Menu](https://github.com/Unity-Technologies/ShaderGraph/wiki/Create-Node-Menu)

## Context Menu

Right clicking within the workspace will open a context menu. Note that right clicking on an item within the workspace, such as a [Node](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node), will open the context menu for that item and not the workspace.

| Item        | Description |
|:------------|:------------|
| Create Node | Opens the [Create Node Menu](https://github.com/Unity-Technologies/ShaderGraph/wiki/Create-Node-Menu) |
| Cut | Cuts selected [Nodes](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) to the clipboard |
| Copy | Copies selected [Nodes](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) to the clipboard |
| Paste | Pastes [Nodes](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) in the clipboard |
| Delete | Deletes selected [Nodes](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) |
| Duplicate | Duplicates selected [Nodes](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) |
| Collapse Previews | Collapses previews on all [Nodes](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) |
| Expand Previews | Expands previews on all [Nodes](https://github.com/Unity-Technologies/ShaderGraph/wiki/Node) |