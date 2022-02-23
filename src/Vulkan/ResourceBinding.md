The key point is that the resource binding operations of the traditional APIs, such as **OpenGL**, is split into two different functions **vkUpdateDescriptorSets** and **vkCmdBindDescriptorSets** in **Vulkan**.  

The **vkUpdateDescriptorSets** is expected to be called on initialization rather than per frame, and thus the **vkCmdBindDescriptorSets**, which is expected to be called per frame, is much faster than the traditional binding APIs, such as **glBindBufferBase**, **glBindTexture**, etc.  

Actually, the **descriptor set** in **Vulkan** can be treated as assets, merely following the vertex buffers of a mesh or the textures of a material.  

Here is a typical pipeline layout of **Vulkan**.  
location              | type                   | readable name               | introduction  
:-                    | :-                     | :-                          | :-  
set = 0               | N/A                    | global descriptor set       | the **vkUpdateDescriptorSets** is called on rendering module initialization  
set = 0 binding = 0   | UNIFORM_BUFFER_DYNAMIC | per frame dynamic offset    | dynamic offset of the unique global_upload_ringbuffer  
set = 0 binding = 1   | UNIFORM_BUFFER_DYNAMIC | per camera dynamic offset   | dynamic offset of the unique global_upload_ringbuffer  
set = 0 binding = ... | UNIFORM_BUFFER_DYNAMIC | per ... dynamic offset      | dynamic offset of the unique global_upload_ringbuffer  
set = 0 binding = 3   | UNIFORM_BUFFER_DYNAMIC | per drawcall dynamic offset | dynamic offset of the unique global_upload_ringbuffer 
set = 0 binding = 4   | COMBINED_IMAGE_SAMPLER | shadow maps                 | for example, the texture array shadow maps of the point lights 
set = 0 binding = 5   | COMBINED_IMAGE_SAMPLER | LUT                         | for example, the global BRDF LUT  
\-\-\-\-\-\-\-\-      | \-\-\-\-\-\-\-\-       | \-\-\-\-\-\-\-\-            | \-\-\-\-\-\-\-\-  
set = 1               | N/A                    | permesh descriptor set      | the **vkUpdateDescriptorSets** is called on mesh initialization  
set = 1 binding = 0   | UNIFORM_BUFFER         | mesh arguments              | the uniform buffer owned by the mesh  
\-\-\-\-\-\-\-\-      | \-\-\-\-\-\-\-\-       | \-\-\-\-\-\-\-\-            | \-\-\-\-\-\-\-\-  
set = 2               | N/A                    | permaterial descriptor set  | the **vkUpdateDescriptorSets** is called on material initialization  
set = 2 binding = 0   | UNIFORM_BUFFER         | material arguments          | the uniform buffer owned by the material  
set = 2 binding = 1   | COMBINED_IMAGE_SAMPLER | albedo map                  | the albedo map owned by the material  

Actually, by using this pipeline layout, the **vkUpdateDescriptorSets** is always called on initialization, and we don't need to call the **vkUpdateDescriptorSets** at all when rendering.  
