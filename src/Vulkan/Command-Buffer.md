# Command Buffer  

In Vulkan, the user usually uses the "Frame_Throttling_Index" [Pipeline Throttling](https://community.arm.com/arm-community-blogs/b/graphics-gaming-and-vr-blog/posts/the-mali-gpu-an-abstract-machine-part-1---frame-pipelining) // which may be different from the "swapchain_image_count"  

## RADV

[RADV](https://docs.mesa3d.org/drivers/radv.html)

// in mesa common command pool framework is used  

the flag VK_COMMAND_POOL_CREATE_RESET_COMMAND_BUFFER_BIT only means vkBeginCommandBuffer implicitly resets the command buffer  

// actually [radv_BeginCommandBuffer](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/radv_cmd_buffer.c#L4854) check whether the buffer has been reset // This means that the flag "VK_COMMAND_POOL_CREATE_RESET_COMMAND_BUFFER_BIT" is ignored

// vkResetCommandBuffer always available

// register the command_buffer_ops [radv_cmd_buffer_ops](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/radv_device.c#L3628)

According to [vk_common_ResetCommandPool](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/vulkan/runtime/vk_command_pool.c#L131) vkResetCommandPool is implemented by vkResetCommandBuffer

the memory of the command buffer is managed by [radv_cmd_buffer_upload](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/radv_private.h#L1661)  

memory free (bo + cs)

[radv_reset_cmd_buffer](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/radv_cmd_buffer.c#L430)  

[radeon_winsys::buffer_destroy](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/radv_cmd_buffer.c#L443)

[radeon_winsys::cs_reset]()  

memory allocate (bo + cs)

// [radv_cmd_buffer_upload_alloc](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/radv_cmd_buffer.c#L574)
// [radv_cmd_buffer_resize_upload_buf](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/radv_cmd_buffer.c#L525) uses "list_add" // more than one buffer object "radeon_winsys_bo"

[radeon_winsys::buffer_create](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/radv_cmd_buffer.c#L536)

// radv_before_draw -> radv_upload_graphics_shader_descriptors 
// radv_flush_vertex_descriptors
// radv_flush_streamout_descriptors
// [radv_flush_constants](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/radv_cmd_buffer.c#L3769) // push constants  

// radv_after_draw

// all emit*** will call [radeon_emit]() // add to the cs

bottom layer  

bo(buffer object) // radeon_winsys_bo // radv_amdgpu_winsys_bo
radeon_winsys::buffer_create -> [radv_amdgpu_winsys_bo_create](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/winsys/amdgpu/radv_amdgpu_bo.c#L1063)  
radeon_winsys::buffer_destroy -> [radv_amdgpu_winsys_bo_destroy](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/winsys/amdgpu/radv_amdgpu_bo.c#L1064)

cs(command space) // radeon_cmdbuf // radv_amdgpu_cs

//  (radeon_cmdbuf::buf)

// implemented by bo (radv_amdgpu_cs::ib_buffer)

radeon_winsys::cs_reset -> radv_amdgpu_cs_reset //  
radeon_winsys::cs_grow -> radv_amdgpu_cs_grow  

## AMDVLK  

TODO  

## Console  

the memory is managed by the user rather than the command buffer  
 
pass the buffer into the "init" method of the command buffer  

and the command buffer will use the "callback" method to allocate more memory when runs out of the memory

