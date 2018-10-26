![](../uploads/Main/Copyof Global Shadow Settings_image_0.png)

| Property          | Function                                                     |
| :---------------- | :----------------------------------------------------------- |
| __Max Distance__  | Maximum shadow distance. This is used for both the last directional cascade boundary and for punctual lights. |
| __Cascade Count__ | Number of cascades for the shadow casting directional light  |
| __Split 1__       | Limit between first and second split (expressed as ratio of max shadow distance) |
| __Solit 2__       | Limit between second and third split (expressed as ratio of max shadow distance) |
| __Split 3__       | Limit between third and last split (expressed as ratio of max shadow distance) |



To help setting things up more easily, users can use the contextual menu to directly create a game object named "Scene Settings" and go from there. This game object is already setup with a default HD Shadow Setting inside a global Volume (it also contains fog and sky default settings).

![](../uploads/Main/Copyof Global Shadow Settings_image_1.png)