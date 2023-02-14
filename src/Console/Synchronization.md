

[radv_cmd_flush_bits](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/radv_private.h#L1173)  

[si_cs_emit_cache_flush](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/si_cmd_buffer.c#L1335)  

GCR (Graphics Cache Rinse)  
[gcr_cntl](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/si_cmd_buffer.c#L1100) 

[PKT3_EVENT_WRITE](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/si_cmd_buffer.c#L1144)  
[PKT3_RELEASE_MEM](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/si_cmd_buffer.c#L1218)  
[PKT3_ACQUIRE_MEM](https://gitlab.freedesktop.org/mesa/mesa/-/blob/22.3/src/amd/vulkan/si_cmd_buffer.c#L1233)  

// AMD RDNA 2 architecture  
[RDNA WhitePaper](https://gpuopen.com/rdna/)  
[RDNA architecture presentation for developers](https://gpuopen.com/rdna/)  

## Execution Dependency

RADV_CMD_FLAG_CS_PARTIAL_FLUSH  

## Memory Dependency  

GPU Cache Hierarchy  
// L1 cache is new which is not presented in RADV code  

// Performs cache operations "at the top of the pipe":  
The GPU can perform cache operations before a specific piece of work starts ("at the top of the pipeline") or after a specific piece of work finishes processing ("at the bottom of the pipeline").  
The acquire_mem packet is so named because the top-of-pipeline operation that it performs puts the cache system into a state that allows the work to perform its memory accesses correctly.  
The MEC will perform the specified cache operation and then stall further operations in this command buffer until the cache operations are complete.  


Type | Description
:-: | :-:  
Write-Combine | allows multiple writes to be combined together in order to improve performance (by "PAGE_WRITECOMBINE" of "Protection Attributes" of "Chapter 13: Windows Memory Architecture" of [Windows via C/C++ Fifth Edition](https://www.microsoftpressstore.com/store/windows-via-c-c-plus-plus-9780735642980))  


Notation | Name | Type | Usage | 
:-: | :-: | :-: | :-:  
I\$ | (Graphics Level 0) Instruction Cache | Read-Only | RADV_CMD_FLAG_INV_ICACHE  
K\$ | (Graphics Level 0) Scalar Cache | Write-Combine | RADV_CMD_FLAG_INV_SCACHE  
V\$ | (Graphics Level 0) Vector Cache | Write-Through | RADV_CMD_FLAG_INV_VCACHE  
CB Data | (Graphics Level 0) Color Block Cache | N/A | RADV_CMD_FLAG_FLUSH_AND_INV_CB 
DB Data | (Graphics Level 0) Depth Block Cache | N/A | RADV_CMD_FLAG_FLUSH_AND_INV_DB  
CB Metadata | (Graphics Level 0) Color Block Metadata Cache | Write-Back | an image with metadata (CMASK, FMASK or DCC) used as the color attachment  
DB Metadata | (Graphics Level 0) Depth Block Metadata Cache | Write-Back | an image with metadata (HTILE) used as the depth attachment  
GL1 | Graphics Level 1 Cache | Write-Through |  N/A  
GL2 | Graphics Level 2 Cache | Write-Combine |	
GLM (GL2 Metadata) | Graphics Level 2 Metadata Cache | Write-Through | an image with metadata (CMASK, FMASK, DCC or HTILE) used as the sampled or storage image  

RADV_CMD_FLAG_INV_ICACHE  
RADV_CMD_FLAG_INV_SCACHE  
RADV_CMD_FLAG_INV_VCACHE  
RADV_CMD_FLAG_FLUSH_AND_INV_CB  
RADV_CMD_FLAG_FLUSH_AND_INV_DB  
RADV_CMD_FLAG_FLUSH_AND_INV_CB_META  
RADV_CMD_FLAG_FLUSH_AND_INV_DB_META  

RADV_CMD_FLAG_INV_L2  
RADV_CMD_FLAG_WB_L2  

RADV_CMD_FLAG_INV_L2_METADATA // the

gfx10_cs_emit_cache_flush  
si_cs_emit_cache_flush

