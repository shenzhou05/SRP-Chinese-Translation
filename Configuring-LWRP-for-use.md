To configure and use LWRP, you must first create the Scriptable Render Pipeline Asset, and edit the Graphics settings for your Project.

## Creating Scriptable Render Pipeline Assets

The Scriptable Render Pipeline Asset controls the global rendering quality settings of your Project and creates the rendering pipeline instance. The rendering pipeline instance contains intermediate resources and the render pipeline implementation.

You can create multiple Pipeline Assets to store settings for different platforms or for different testing environments.

To create a Render Pipeline Asset:

1. In the Editor, go to the Project window, and navigate to a directory outside of the Scriptable Render Pipeline Folder. 

2. Right-click in the Project window, and select __Create__ &gt; __Render Pipeline__. Select __Lightweight__. Click __Render Pipeline/Pipeline Asset__.


## Editing Graphics settings for your Project

1. In the Project window, navigate to a directory outside of the _Scriptable Render Pipeline_ folder. 
2. Right-click in the Project window, and select __Create__ > __Render Pipeline__ > __Lightweight__ > __Pipeline Asset__.
3. Navigate to __Edit__ > __Project Settings__ > __Graphics__. 
4. In the __Render Pipeline Settings__ field, add the Lightweight Render Pipeline Asset you created earlier.

**Tip:** Always store your new Render Pipeline Asset outside of the _Scriptable Render Pipeline_ folder. This ensures that your Lightweight settings are not lost when you merge new changes from the SRP GitHub repository.

