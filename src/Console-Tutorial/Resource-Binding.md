# Resource Binding  

In legacy OpenGL or Direct3D11 APIs, resources can be bound to each slot separately.  

Evidently, the driver of the legacy OpenGL or Direct3D11 APIs needs to allocate a block of memory, which contains all resource bindings, from the command buffer for each draw call. And the driver needs to provide the address of the allocated memory to the hardware before the draw call is issued.  

Analogous to the pipeline state, it is not efficient to allocate a block of memory from the command buffer for each draw call. It is more efficient for the application to allocate and initialize a block of memory in advance, and reuse the memory at each frame.  

This is the idea of of the (shader visible) descriptors in modern Vulkan or Direct3D12 APIs. The application allocates and initailzes a block of memory in advance, and provides the address of the memory to the hardware before the draw call is issued.

N/A | allocate memory  | initailze memory | bind memeory 
:-: | :-: | :-: | :-:  
Vulkan | vkCreateDescriptorPool <br/> vkAllocateDescriptorSets | vkUpdateDescriptorSets | vkCmdBindDescriptorSets   
Direct3D12 | ID3D12Device::CreateDescriptorHeap | ID3D12Device::CreateShaderResourceView <br/> ID3D12Device::CreateSampler | ID3D12GraphicsCommandList::SetDescriptorHeaps <br/> ID3D12GraphicsCommandList::SetGraphicsRootConstantBufferView <br/> ID3D12GraphicsCommandList::SetGraphicsRootDescriptorTable   

In console, an analog of the **ID3D12RootSignature** in Direct3D12 can be used.  
