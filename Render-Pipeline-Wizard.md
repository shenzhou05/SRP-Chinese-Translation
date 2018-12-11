This little wizard will help you checking your configuration set in editor is compatible with HD render pipeline.

![[Wizard screen shot]](https://github.com/Unity-Technologies/ScriptableRenderPipeline/blob/0421c562e95867c39078a09b59475bfe33bbba53/com.unity.render-pipelines.high-definition/Documentation~/Images/Wizard.png?raw=true)

## Populate / Reset
This will allows you to populate the folder defined with default resources needed in HD render pipeline. By default, the folder will be "HDRPProjectSettings" which coule be modified before populating. If asset already exist, they will be overridden.

### List of created assets:
* **DefaultSceneRoot:** it allows you to have a scene configured for HD render pipeline each time you do a **File > New Scene** and also when you create asset in project windows **Create > HD Template Scene**
* **DefautRenderingSettings:** rendering settings's profile which is used in the DefaultSceneRoot.
* **DefautPostprocessingSettings:** post-processing settings's profile which is used in the DefaultSceneRoot.
* **HDRenderPipellineAsset:** main entry point for HD render pipeline. Every resources will be found by him. It is provided with resources already configured.
* **DefaultDiffusionProfileSettings:** post-processing settings's profile which is used in the HDRenderPipellineAsset.

## Configuration checker
Then you will find every requested configuration for HD render pipeline working well. Each line is a test. If there is any issue, it is explained and have a quick fix button displayed. They will help you to quickly fix your project. 
If a resources is missing you can load one or create it. In case of creation, it will put resources in the same folder than the Populate/Reset button, overriding element if needed.

### Important note:
The wizard can only be shown if the package have compiled. One of the main issue would be if _Script runtime version_ is not set to .Net 4.x or higher. You must fix it manually in order to be able compile the package and thus the wizard cannot resolve this for you. However, if the package have already compiled once, _Script runtime version_'s fix button will work and allows you to fix this issue.
