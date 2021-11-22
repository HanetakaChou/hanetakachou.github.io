# Scene


## NVIDIA PRO PIPELINE

By \[Tavenrath 2013\], the [NVIDIA PRO PIPELINE](https://developer.nvidia.com/nvidia-pro-pipeline) consists of the following stages: SceneGraph -> SceneTree -> ShapeList.  

Since there is no document for **NVIDIA PRO PIPELINE**, we may refer to the documents of [NVIDIA SceniX](https://developer.nvidia.com/scenix-details).

### Scene Graph  

The [dp::sg::core::Scene](https://github.com/nvpro-pipeline/pipeline/blob/master/dp/sg/core/Scene.h) represents the **scene graph** which is also referred to as the **user tree** by **NVIDIA SceniX** and **user-oriented tree** by \[Akenine-Moller 2018\] / 19.1.5 Scene Graphs.  

However, we should note that the **scene graph** and **scene tree** are diffirent. The **scene graph** is a DAG which may share the subtree and thus is not efficient. And, in real time rendering, we usually use the **scene tree** instead, which only shares the leaf nodes (\[Akenine-Moller 2018\] / 19.1.5 Scene Graphs).  

The [dp::sg::core::Node](https://github.com/nvpro-pipeline/pipeline/blob/master/dp/sg/core/Node.h) represents all nodes (both the internal nodes and the leaf nodes) of the **scene graph**.

And the [dp::sg::core::Group](https://github.com/nvpro-pipeline/pipeline/blob/master/dp/sg/core/Group.h) represents the internal node which provides the ability to group **dp::sg::core::Node**-derived objects as children.  

There are several **dp::sg::core::Group**-derived internal nodes: [dp::sg::core::Transform](https://github.com/nvpro-pipeline/pipeline/blob/master/dp/sg/core/Transform.h), [dp::sg::core::LOD](https://github.com/nvpro-pipeline/pipeline/blob/master/dp/sg/core/LOD.h) (\[Akenine-Moller 2018\] / Figure 19.34), [dp::sg::core::Switch](https://github.com/nvpro-pipeline/pipeline/blob/master/dp/sg/core/Switch.h), [dp::sg::core::Billboard](https://github.com/nvpro-pipeline/pipeline/blob/master/dp/sg/core/Billboard.h) ([Akenine-Moller 2018\] / 13.6. Billboarding).  

There are several **dp::sg::core::Node**-derived but **NOT** **dp::sg::core::Group**-derived leaf nodes: [dp::sg::core::GeoNode](https://github.com/nvpro-pipeline/pipeline/blob/master/dp/sg/core/GeoNode.h), [dp::sg::core::LightSource](https://github.com/nvpro-pipeline/pipeline/blob/master/dp/sg/core/LightSource.h), [dp::sg::core::ClipPlane](https://github.com/nvpro-pipeline/pipeline/blob/master/dp/sg/core/ClipPlane.h), [dp::sg::core::ClipPlane](https://github.com/nvpro-pipeline/pipeline/blob/master/dp/sg/core/ClipPlane.h).

### Scene Tree  


## Pixar Hydra


## References
\[Harrison 2010\] [Brian Harrison, Michael Morrison. "BUILDING CUTTING-EDGE REALTIME 3D APPLICATIONS WITH NVIDIA SCENIX." GTC 2010.](https://on-demand.gputechconf.com/gtc/2010/video/S12308-Building-Cutting-Edge-Realtime-3D-Apps-with-NVIDIA-SceniX.flv)  
\[Tavenrath 2013\] [Markus Tavenrath, Christoph Kubisch. "Advanced Scenegraph Rendering Pipeline." GTC 2013.](https://on-demand.gputechconf.com/gtc/2013/presentations/S3032-Advanced-Scenegraph-Rendering-Pipeline.pdf)  
\[Akenine-Moller 2018\] [Tomas Akenine-Moller, Eric Haines, Naty Hoffman, Angelo Pesce, Michal Iwanicki, Sebastien Hillaire. "Real-Time Rendering Fourth Edition." CRC Press 2018.](https://www.realtimerendering.com/)  
\[Elkoura 2019\] [George Elkoura, Sebastian Grassia, Sunya Boonyatera, Alex Mohr, Pol Jeremias-Vila, Matt Kuruc. "A deep dive into universal scene description and hydra." SIGGRAPH 2019.](http://graphics.pixar.com/usd/files/Siggraph2019_Hydra.pdf)