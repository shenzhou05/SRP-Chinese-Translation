# 可编辑渲染管线
![](https://blogs.unity3d.com/wp-content/uploads/2018/01/image5_rs.png)
## 什么是可编程渲染管线 (SRP)

SRP是一个新的Unity特性，它可以让艺术家和开发者完全控制Unity渲染管线。这是一种先进的工具，使得我们可以在Unity中创建高保真画质。SRP允许开发者编写c#脚本来控制Unity渲染每一帧的方式。通过将Unity渲染管线暴露给c#脚本， Unity不再是一个“黑盒”，因为开发人员可以看到并控制渲染过程中发生的事情。

开发人员可以使用两个内建管线(轻量管线LWRP和高清管线HDRP)，这两种拓展管线也是SRP提供的一部分。开发者可以从头开始开发自己的管线，或者修改提供的管线，使其适应自己的需求。

这个wiki包含了SRP、LWRP和HDRP的beta版文档。关于此wiki的文档可能会更改，而且可能是不完整的。在目前阶段，我们正在寻求反馈，而且当前SRP的特性是不完整的，并且可能会发生变化(API、UX、作用域)。SRP还没有准备好生产，也没有得到常规的Unity支持。您可以直接向论坛提出问题和反馈。(链接:https://forum.unity.com/categories/betas-experimental-features.86/)