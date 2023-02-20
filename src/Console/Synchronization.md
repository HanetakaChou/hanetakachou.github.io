# Synchronization  

## PM4 Packet

[PKT3_EVENT_WRITE](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/si_cmd_buffer.c#L1144)  

[PKT3_ACQUIRE_MEM](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/si_cmd_buffer.c#L1233)  

[PKT3_RELEASE_MEM](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/si_cmd_buffer.c#L1218)  

[PKT3_EVENT_WRITE_EOP](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/si_cmd_buffer.c#L1047)  

// flush cache
PKT3_WAIT_REG_MEM  

But the event_write packet does NOT make the CP stall.  

Usually, the acquire_mem packet can be used to mantually make the CP stall until the events triggered by the event_write packet have been processed. 

// acquire_mem: the cache op (cb metadata or db metadata is NOT supported) is split into cb_db_op (cb or db caches) and gcr_cntl (Graphics Cache Rinse - Control, no cb or db caches)  

But sometimes we may have a no-depth no-color PS, the event_write_eop and wait packets packets should be used to make mantually the CP stall.   

## Wait Synchronization

TODO | TODO  
:- | :-  
TODO | RADV_CMD_FLAG_VS_PARTIAL_FLUSH  
TODO | RADV_CMD_FLAG_PS_PARTIAL_FLUSH  
TODO | RADV_CMD_FLAG_CS_PARTIAL_FLUSH  

The GPU has some internal signalling.  
The command packet (PKT3_EVENT_WRITE) throws an event down the pipeline and stalls the CP(command processor) until the signal arrives.  
This is supported by Compute Shader (RADV_CMD_FLAG_CS_PARTIAL_FLUSH), Pixel Shader (RADV_CMD_FLAG_PS_PARTIAL_FLUSH) and Vertex Shader (RADV_CMD_FLAG_VS_PARTIAL_FLUSH).  


cache flush  
signalling that an operation has finished  
waiting for the signal

[PKT3_EVENT_WRITE](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/si_cmd_buffer.c#L1144)  



[SI_CONTEXT_PFP_SYNC_ME](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/gallium/drivers/radeonsi/si_gfx_cs.c#L796)  

CPG (Command Processor Graphics) = PFP (Pre-Fetch Parser) V_580_CP_PFP +  ME (Micro Engine) 

[V_580_CP_PFP](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/si_cmd_buffer.c#L1234)  
[V_580_CP_ME](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/radv_device.c#L4574)  


PFP - ME - // wait on early stage is ususaly safe // wait on later stage is usually more efficient  
// PFP will ask GE to prefetch index data

## Cache Synchronization  

### GPU Cache Hierarchy  

```graphviz
```

The flush operation makes the data which has been written visible to other units. Evidently, the **read-only** or **walk-through** caches do NOT support the flush operation. The invalidate operation makes the data which will be read is NOT stale.  
The supported flush and invalidate operations can be checked by [radv_cmd_flush_bits](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/radv_private.h#L1173), [si_cs_emit_cache_flush](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/si_cmd_buffer.c#L1335) and [gcr_cntl (Graphics Cache Rinse - Control)](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/si_cmd_buffer.c#L1100) in [RADV](https://docs.mesa3d.org/drivers/radv.html).  

Cache Notation | Cache Name | Cache Type | Cache Usage | Flush Operation Name RADV | Flush Operation Packet RADV | Flush Operation Usage | Invalidate Operation RADV | Invalidate Operation Usage  
:- | :- | :- | :- | :- | :-  | :- | :- | :-  
I\$ | (Graphics Level 0) Instruction Cache | Read-Only | TODO | N/A | N/A | N/A | RADV_CMD_FLAG_INV_SCACHE |  | TODO  
K\$ (GL0S) | (Graphics Level 0) Scalar Cache | Write-Back | TODO | X_XXX_GLK_WB | TODO | TODO | RADV_CMD_FLAG_INV_KCACHE | TODO  
V\$ (GL0V) | (Graphics Level 0) Vector Cache | Write-Through | TODO | N/A | N/A | N/A | RADV_CMD_FLAG_INV_VCACHE | TODO  
CBD\$ (CB Data) | (Graphics Level 0) Color Block Cache | Write-Back | an image is accessed as the color attachment | RADV_CMD_FLAG_FLUSH_AND_INV_CB | TODO | an image has been written as the color attachment and will be read by another usage <br /> ------- <br /> the data will be flushed to GL1 and written directly to GL2 | RADV_CMD_FLAG_FLUSH_AND_INV_CB | TODO  
DBD\$ (DB Data) | (Graphics Level 0) Depth Block Cache | Write-Back | an image is accessed as the depth attachment | RADV_CMD_FLAG_FLUSH_AND_INV_DB | TODO | an image has been written as the depth attachment and will be read by another usage <br /> ------- <br /> the data will be flushed to GL1 and written directly to GL2 | RADV_CMD_FLAG_FLUSH_AND_INV_DB | TODO  
CBM\$ (CB Metadata) | (Graphics Level 0) Color Block Metadata Cache | Write-Back | an image with metadata (CMASK, FMASK or DCC) is accessed as the color attachment | RADV_CMD_FLAG_FLUSH_AND_INV_CB_META | PKT3_EVENT_WRITE | an image with metadata (CMASK, FMASK or DCC) has been written as the color attachment and will be read by another usage <br /> ------- <br /> the data will be flushed to GL1 and written directly to GL2 | RADV_CMD_FLAG_FLUSH_AND_INV_CB_META | TODO  
DBM\$ (DB Metadata) | (Graphics Level 0) Depth Block Metadata Cache | Write-Back | an image with metadata (HTILE) is accessed as the depth attachment  | RADV_CMD_FLAG_FLUSH_AND_INV_DB_META | PKT3_EVENT_WRITE | an image with metadata (HTILE) has been written as the depth attachment and will be read by another usage <br /> ------- <br /> the data will be flushed to GL1 and written directly to GL2 | RADV_CMD_FLAG_FLUSH_AND_INV_DB_META | TODO  
GL1 | Graphics Level 1 Cache | Write-Through | communication inside GPU | N/A | N/A | N/A | X_XXX_GL1_INV | the data has been written to GL1 by the flush operation and will be read by GPU <br /> ------- <br /> the data has been written by one computer shader and will be read by another computer shader (there are multiple GL0 and GL1 caches but the coherency is NOT maintained for computer shaders)  
GL2 | Graphics Level 2 Cache | Write-Back |	communication between GPU and CPU | RADV_CMD_FLAG_WB_L2 | PKT3_ACQUIRE_MEM | the data has been written by GPU and will be read by CPU | RADV_CMD_FLAG_INV_L2 | the data without the "VK_MEMORY_PROPERTY_HOST_COHERENT_BIT" has been written by CPU and will be read by GPU   
GLM (GL2 Metadata) | Graphics Level 2 Metadata Cache | Write-Through | an image with metadata (CMASK, FMASK, DCC or HTILE) accessed as the sampled or storage image | N/A | N/A | N/A | RADV_CMD_FLAG_INV_L2_METADATA | the metadata of the image has been written to GL2 by the flush operation and the image will be accessed as the sampled or storage image <br /> ------- <br /> it is NOT necessary to invalidate the GLM when the data is accessed as the buffer since the data will NOT go through the GLM  

The CB Metadata and the DB Metadata can only be flushed by event_write packet. 

// and there is a hardware restriction: if the metadata are flushed, the the matching data are forced to flushed as well  

But the event_write packet does NOT make the CP stall.  

Usually, the acquire_mem packet can be used to mantually make the CP stall until the events triggered by the event_write packet have been processed. 

// acquire_mem: the cache op (cb metadata or db metadata is NOT supported) is split into cb_db_op (cb or db caches) and gcr_cntl (Graphics Cache Rinse - Control, no cb or db caches)  

But sometimes we may have a no-depth no-color PS, the event_write_eop and wait packets packets should be used to make mantually the CP stall.  

### GL2

The GL2 is only used for the communication between GPU and CPU (for example, implementing the VkFence and the VkSemaphore).  

By [si_cache_policy](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/gallium/drivers/radeonsi/si_pipe.h#L285) of RADV, we have the GL2 cache policies.  

Policy Name | TODO  
:- | :-   
LRU | TODO  
BYPASS | TODO  
STREAM | TODO  

**write-combine** which allows multiple writes to be combined together in order to improve performance (by "PAGE_WRITECOMBINE" of "Protection Attributes" of "Chapter 13: Windows Memory Architecture" of [Windows via C/C++ Fifth Edition](https://www.microsoftpressstore.com/store/windows-via-c-c-plus-plus-9780735642980))  

