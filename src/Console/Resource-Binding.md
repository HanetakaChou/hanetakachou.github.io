# Resource Binding  

traditional: allocate memory for shader registers from command buffer on the fly  

shader resource table: allocate memory for shader registers in advance (vkUpdateDescriptorSets) and bind the memory on the fly (vkCmdBindDescriptorSets)  
