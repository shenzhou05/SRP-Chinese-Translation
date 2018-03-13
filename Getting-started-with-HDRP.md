# Getting Started with High Definition Render Pipeline

This page details the initial setup of a project using the High Definition Render Pipeline (HDRP) and notes on upgrading existing projects to HDRP. 
## Setting up a new Project

### Using Unity Hub
To set up a new HDRP project using Unity Hub, click the New button, then select High Definition - Preview from the Template dropdown box. After clicking Create Project, Unity will automatically create a Project with the High Definition Render Pipeline package installed. 

### Upgrading an existing Project
To upgrade an existing Project, you must first download the High Definition Render Pipeline using the Package Manager UI. 

Navigate to Window > Package Manager to open the Package Manager UI. Then click the All button to open the packages list. 

Left click on Render-pipelines.high-definition  to select it, then click the Install button to add HDRP to your project. 

After you have installed HDRP from the Package Manager UI you must add the HDRP  Asset to the Scriptable Render Pipeline Graphics settings field. 

Navigate to Edit > Settings > Graphics Settings, then Assign the HDRP Asset to the Scriptable Render Pipeline field by dragging in the HDRP Asset, or using the radio button to select the Asset from the popup window. 

## Upgrading Shaders

The built-in Unity shaders are incompatible with Scriptable Render Pipelines, as such, any preexisting Shaders in your project must be updated to work with the HDRP.

Navigate to Edit > Render Pipelines > HDRP > Upgrade > Upgrade shaders to run the automatic upgrade script. This script with automatically update all preexisting shaders in your project to the new HDRP shaders. 
