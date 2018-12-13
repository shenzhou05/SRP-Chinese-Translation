The HDRP Lit shaders (Lit, LitTessellation, Layered Lit, Layered Lit Tessellation) allow you to use displacement. 

**Displacement** is the action of pushing a vertex or a pixel by a certain distance in the direction of the vertex or pixel's normal.

| Displacement mode                                        |                                                              |
| -------------------------------------------------------- | ------------------------------------------------------------ |
| None                                                     | No displacement is applied.                                  |
| Vertex displacement (not in tessellation shaders)        | Vertices of the mesh are displaced according to the **Height Map** and the **amplitude** or **Min Max** set in the **Inputs** section. |
| Pixel displacement (not in tessellation shaders)         | Pixels of the mesh's surface are displaced according to the **Height Map** and the **amplitude** set in the **Inputs** section. |
| Tessellation displacement (only in tessellation shaders) | Tessellation subdivides the mesh and adds vertices accordingly to the tessellation options (see below). These vertices are then displaced according to the **Height Map** and the **amplitude** or **Min Max** set in the **Inputs** section. This technique is used to add details to the mesh at the cost of performance. |

| Displacement options             |                                                              |
| -------------------------------- | ------------------------------------------------------------ |
| Lock with object scale           | When enabled, the amplitude of the displacement is modulated by the scale of the object. This allows you to preserve the ratio between the displacement's amplitude and the scale of your object. |
| Lock with height map tiling rate | When enabled, the amplitude of the displacement is modulated by the tiling of the height map. This allows you to preserve the ratio between the displacement's amplitude and the scale of the texture. |

| Pixel displacement options | (Pixel displacement only)                                    |
| -------------------------- | ------------------------------------------------------------ |
| Minimum steps              | Minimum number of texture samples performed for pixel displacement. |
| Maximum steps              | Maximum number of texture samples performed for pixel displacement. |
| Fading mip level start     | Mip level at which the pixel displacement effect starts fading out. |
| Primitive length           | Length of the mesh on which the displacement mapping is being applied. |
| Primitive width            | Width of the mesh on which the displacement mapping is being applied. |
| Depth offset               | Enabling this will modify the depth buffer according to the pixel displacement. This allows effects that rely on the depth buffer (like contact shadows and SSAO) to capture pixel displacement details. |

| Tessellation options                        | (Tessellation shaders only)                                  |
| ------------------------------------------- | ------------------------------------------------------------ |
| Tessellation mode                           |                                                              |
| None                                        | The vertices are only displaced if a Height map is used.     |
| Phong                                       | The vertices created by tessellation are displaced along their normals according to the **Shape factor** whether a Height map is used or not. This is useful when tessellation is used on an organic object in order to smooth the original polygons of the mesh. |
| Tessellation factor                         | Number of iterations of subdivisions applied to the mesh.    |
| Start fade distance                         | Distance at which tessellation starts disappearing.          |
| End fade distance                           | Distance at which tessellation is no longer visible and the initial mesh is rendered. |
| Triangle size                               | Minimum size in pixel that a triangle can have. When this size is reached on a triangle, increasing the tessellation factor won't subdivide this triangle anymore. |
| Shape factor (phong tessellation mode only) | Strength of the phong displacement. 0 is the same as phong displacement disabled. Increasing the value towards one displaces more and more the vertices added by tessellation along their normals. |
| Triangle culling epsilon                    | Threshold used for backface culling of tessellated polygons. -1 means backface culling is disabled. Higher values mean more aggressive backface culling and better performance. Too high values can discard too many polygons on the silhouette of tessellated meshes. |

