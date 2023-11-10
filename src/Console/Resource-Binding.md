# Resource Binding  

traditional: allocate memory for shader registers from command buffer on the fly  

shader resource table: allocate and initialize memory for shader registers in advance (vkAllocateDescriptorSets and vkUpdateDescriptorSets), and bind the memory on the fly (vkCmdBindDescriptorSets)  
