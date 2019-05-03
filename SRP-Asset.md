SRP资源包含用户在配置管道时使用的接口，当Unity第一次执行渲染时，它将调用资源的`InternalCreatePipeline` ，并且这个资源需要返回可用的SRP实例。

渲染管线资源是一个ScriptableObject，这意味着它可以是一个项目资源，并可保存到一些类似版本控制的插件中。如果您希望保存一个配置供其他人使用，那么您需要在项目中创建一个相应的配置资源。可以像其他任何ScriptableObject一样通过脚本创建管线资源，然后通过资源数据库(AssetDatabase)API保存。

要在项目中设置启用的SRP资源，您需要通过图形设置来设置该资源。设置资源引用后，将在项目中“启用”SRP渲染，并且渲染方式将从标准的Unity渲染转换到已编辑的配置中。

## 一个简单的资源示例
资源的职责是包涵配置并返回可用于执行渲染的管线实例。如果更改了资源上的设置，则已创建的所有实例都将被销毁，并使用下一帧渲染的新设置创建新实例。

下面的示例显示了一个简单的管线资源类。它包含一种颜色配置，创建的实例将使用该颜色清除屏幕。还有一些仅限编辑器使用的代码可以帮助用户创建一种可在项目中使用的资源，这一点很重要，因为您需要能够在“图形设置”窗口中设置此资源。

```C#
[ExecuteInEditMode]
public class BasicAssetPipe : RenderPipelineAsset
{
    public Color clearColor = Color.green;

#if UNITY_EDITOR
    // 创建一个简单的管线
    [UnityEditor.MenuItem("SRP-Demo/01 - Create Basic Asset Pipeline")]
    static void CreateBasicAssetPipeline()
    {
        var instance = ScriptableObject.CreateInstance<BasicAssetPipe>();
        UnityEditor.AssetDatabase.CreateAsset(instance, "Assets/BasicAssetPipe.asset");
    }
#endif

    // 函数返回一个管线的实例
    protected override IRenderPipeline InternalCreatePipeline()
    {
        return new BasicPipeInstance(clearColor);
    }
}
```

## 一个复杂的资源示例
除了返回和实例以及保存配置数据外，资源还可用于许多辅助函数使用，例如：
* 创建三维对象时使用的默认材质
* 创建二维对象时使用的默认材质
* 创建粒子系统时使用的默认材质
* 创建地形系统时使用的默认材质

它本质上提供了一个Hook点，确保从头到尾编辑器体验是无误的。如果您构建了一个管线，并且希望它像原有的Unity管道一样集成和“真实”，那么这些步骤是必须的。

```
Example
```