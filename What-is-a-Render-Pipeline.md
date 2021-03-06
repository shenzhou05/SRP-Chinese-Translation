“渲染管线”是一个概括的术语，用于描述将物体渲染到屏幕上的一些技术。它在非常高的层面上包括:
* 剔除
* 渲染对象
* 后处理

除了这些高级概念之外，每个渲染任务还可以进一步分解，这取决于您希望如何执行它们。例如，渲染对象可以使用:
* 多pass渲染 - 每一盏灯每个物体使用一个pass
* 单pass渲染 - 每个物体一个pass
* 延迟渲染 - 渲染表面属性到G-buffer中，执行屏幕空间照明

在编写自定义SRP时，您需要在这些方案中做出选择。每种方法都有一些您应该考虑的权衡，而且对于给定的项目，没有一种方法是绝对完美的。