The asset contains the interface that users use when configuring a pipeline, when Unity performs rendering for the first time it will call `InternalCreatePipeline` on the pipeline. 

The render pipeline asset is a ScriptableObject and if you wish to use this pipeline for rendering you need to create one in your project. These can be created just like any other ScriptableObject. When the asset is created it can be set in the Graphics Settings for the project.

The responsibility of the asset is to return an instance of a pipeline that can be used for performing rendering. If a setting on the asset is changed all instances that have been created are destroyed and a new instance is created with the new settings.

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