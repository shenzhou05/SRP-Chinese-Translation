The asset contains the interface that users use when configuring a pipeline, when Unity performs rendering for the first time it will call `InternalCreatePipeline` on the asset and the asset is required to return a usable instance. 

The render pipeline asset is a ScriptableObject which means that it can be a project asset and saved to version control and similar. I you wish to save a configuration for others to use then you need to create one in your project. Pipeline assets can be created just like any other ScriptableObject via script and then saved via the asset database API. 

To set an SRP asset as enabled in your project you need to set the asset via the GraphicsSettings. Setting the asset reference here will 'enable' SRP rendering in your project and rendering will be diverted from standard Unity rendering to the configuration you have scripted.

## An Simple Asset Example
The responsibility of the asset is to contain configuration and to return an instance of a pipeline that can be used for performing rendering. If a setting on the asset is changed all instances that have been created are destroyed and a new instance is created with the new settings for the next frame of rendering.

The example below shows a simple pipeline asset class. It contains a color that will be used by the created instance to clear the screen. There is also some editor only code that assists a user in creating an asset that can live in the project, this is important as you need to be able to set this asset in the graphics settings window.

```C#
[ExecuteInEditMode]
public class BasicAssetPipe : RenderPipelineAsset
{
    public Color clearColor = Color.green;

#if UNITY_EDITOR
    // Call to create a simple pipeline
    [UnityEditor.MenuItem("SRP-Demo/01 - Create Basic Asset Pipeline")]
    static void CreateBasicAssetPipeline()
    {
        var instance = ScriptableObject.CreateInstance<BasicAssetPipe>();
        UnityEditor.AssetDatabase.CreateAsset(instance, "Assets/BasicAssetPipe.asset");
    }
#endif

    // Function to return an instance of this pipeline
    protected override IRenderPipeline InternalCreatePipeline()
    {
        return new BasicPipeInstance(clearColor);
    }
}
```

## A complete asset example
In addition to returning and instance and holding configuration data the asset is used for a number of helper functions, things like:
* Default material to use when creating 3d objects
* Default material to use when creating 2d objects
* Default material to use when creating particle systems
* Default material to use when creating terrain systems

Essentially providing a hook points to ensure that the end to end editor experience feels right. If you construct a pipeline and would like it to feel integrated and 'real' like the existing Unity pipelines these steps area  requirement.

```
Example
```