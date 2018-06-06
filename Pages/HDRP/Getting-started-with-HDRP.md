# Getting Started with High Definition Render Pipeline

This page details the initial setup of a project using the High Definition Render Pipeline (HDRP) and notes on upgrading existing projects to HDRP. 
## Setting up a new Project

### Using Unity Hub
Follow the steps below to set up a new HDRP project using Unity Hub.

1. On the Projects screen click the New button
2. Select High Definition - Preview from the Template drop-down box
3. Click Create Project

After clicking Create Project, Unity will automatically create a Project with the High Definition Render Pipeline package installed. 

## Upgrading an Existing Project
To upgrade an existing Project, you must first download the High Definition Render Pipeline using the Package Manager UI. 

1. Navigate to **Window > Package Manager** to open the Package Manager UI. Then click the All button to open the packages list. 
2. Left click on Render-pipelines.high-definition  to select it, then click the Install button to add HDRP to your project. 

After you have installed HDRP from the Package Manager UI you must add the HDRP  Asset to the Scriptable Render Pipeline Graphics settings field. 

3. Navigate to Edit > Settings > Graphics Settings, then Assign the HDRP Asset to the Scriptable Render Pipeline field by dragging in the HDRP Asset, or using the radio button to select the Asset from the popup window. 

## Building from source code

The latest version of the Scriptable Render Pipeline (SRP) repo can be found at the following link: https://github.com/Unity-Technologies/ScriptableRenderPipeline

### Github Desktop or Git command line tools

#### Cloning the repo using the GitHub Desktop App: 
Open the GitHub Desktop App and click Clone a Repository. 

Click the URL tab in the Clone a Repository window
Enter the following URL: https://github.com/Unity-Technologies/ScriptableRenderPipeline
Click the Choose… button to navigate to your project’s Asset folder. 
Click the Clone button. 

After the repo has been cloned you must run the following console commands from the ScriptableRenderPipeline folder:

`git checkout Unity-2018.1.0b2 (or the latest tag)`

`git submodule update --init --recursive --remote`

#### Cloning the repo using Git console commands:
Enter the following commands in your console application of choice:  
`cd <Path to your Unity project>/Assets`

`git clone https://github.com/Unity-Technologies/ScriptableRenderPipeline`

`cd ScriptableRenderPipeline`

`git checkout Unity-2018.1.0b2 (or the latest tag)`

`git submodule update --init --recursive --remote`

Once you have cloned the repo, re-open your project and follow the below instructions: 

Navigate to **Edit > Project Settings > Graphics** and add the HDRenderPipelineAsset Asset to the Render Pipeline Settings field. 

Create a copy of the HDRenderPipelineAsset and store it outside of the Scriptable Render Pipeline folder. This ensures that your HDRP settings are not lost when merging new changes from the SRP repo. 
HDRP will be ready to use in your project after following the above instructions.

## Upgrading Shaders

The built-in Unity shaders are incompatible with Scriptable Render Pipelines, as such, any preexisting Shaders in your project must be updated to work with the HDRP.

Navigate to **Edit > Render Pipelines > Upgrade Project Materials to High Definition Materials** to run the automatic upgrade script. This script with automatically update all preexisting shaders in your project to the new HDRP shaders. 
