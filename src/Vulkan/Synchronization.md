
## Mental model

All commands are executing in all stages defined by "VkPipelineStageFlag" while the command may do nothing in some of these stages.  
For example, evidently, the copy command does nothinng in the "COMPUTE_SHADER" stage.  
And there are two typical stages "TOP_OF_PIPE" and "BOTTOM_OF_PIPE" in which all commands do nothing.  

In the mental model, the command is executing in these stages according to the [logical order]().  
For example, logically, the copy command is  executing in the "TOP_OF_PIPE" stage first, the "COMPUTE_SHADER" stage next, the "TRANSFER" stage later and the "BOTTOM_OF_PIPE" stage finally.  
Actually, the copy command  does nothing in the "TOP_OF_PIPE", "COMPUTE_SHADER" and "BOTTOM_OF_PIPE" stages.  
And, in my opinion, the "TOP_OF_PIPE" and "COMPUTE_SHADER" stages are the equivalent for the copy command.

And thus, we may use the "COMPUTE_SHADER" stage to define the execution dependency to make the copy command wait for some other jobs.  
This execution dependency is definitely legal and the "TRANSFER" stage of the copy command **happens after** the these jobs since the "TRANSFER" stage of the copy command logically **happens after** "COMPUTE_SHADER" stage of the same copy command.  
However, the execution dependency doesn't imply the memory dependency and the "TRANSFER" stage of the copy command may not be able to use the data produced by these jobs.  

```c++
vkCmdDispatch

vkCmdPipelineBarrier(..., VK_PIPELINE_STAGE_COMPUTE_SHADER_BIT, ...

// Evidently, the "COMPUTE_SHADER" stage of this dispatch command happens after the dispatch command which is before the barrier.
vkCmdDispatch

// The "TRANSFER" stage of this copy command happens after the dispatch command which is before the barrier as well since the "TRANSFER" stage of the copy command logically happens after "COMPUTE_SHADER" stage of the same copy command.  
// However, this copy command may not be able to use the data produced by the dispatch command which is before the barrier since the execution dependency doesn't imply the memory dependency.
vkCmdCopyBufferToImage
```