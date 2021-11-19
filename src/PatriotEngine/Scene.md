# Scene


## NVIDIA PRO PIPELINE

By \[Tavenrath 2013\], the [NVIDIA PRO PIPELINE](https://developer.nvidia.com/nvidia-pro-pipeline) consists of the following stages: SceneGraph -> SceneTree -> ShapeList.  

Since there is no document for **NVIDIA PRO PIPELINE**, we may refer to the documents of [NVIDIA SceniX](https://developer.nvidia.com/scenix-details).

### Scene Graph  

The [dp::sg:core:Scene](https://github.com/nvpro-pipeline/pipeline/blob/master/dp/sg/core/Scene.h) represents the **Scene Graph** which is also referred to as the **User Tree** by **NVIDIA SceniX**.  
However, we should note that the Graph and Tree are diffirent since there may be shared subtree inside the Graph.

## References
\[Harrison 2010\] [Brian Harrison, Michael Morrison. "BUILDING CUTTING-EDGE REALTIME 3D APPLICATIONS WITH NVIDIA SCENIX." GTC 2010](https://on-demand.gputechconf.com/gtc/2010/video/S12308-Building-Cutting-Edge-Realtime-3D-Apps-with-NVIDIA-SceniX.flv)  
\[Tavenrath 2013\] [Markus Tavenrath, Christoph Kubisch. "Advanced Scenegraph Rendering Pipeline." GTC 2013.](https://on-demand.gputechconf.com/gtc/2013/presentations/S3032-Advanced-Scenegraph-Rendering-Pipeline.pdf)  
