
# ReSTIR (Reservoir-Based Spatiotemporal Importance Resampling)  

## Reservoir Sampling  

### Basic Reservoir Sampling  

By "A.2 Reservoir Sampling" of [PBR Book V4](https://www.pbr-book.org/4ed/Sampling_Algorithms/Reservoir_Sampling#), we have the **basic reservoir sampling**.  
   
We sequentially process each **sample** from the **stream**. The total length of the **stream** can indeed be infinite which is too large to be stored in the memory.   

We assume that we have processed **n** **samples**. This means that the number of the **seen samples** is **n**. For the **basic reservoir sampling**, the **reservoir** can hold at most **1** **reservoir sample**, and the first **1** **seen** **sample** is always selected to initialize the **reservoir**. For each subsequent **seen** **candidate sample**, we decide whether or not it should be selected to replace the existing **sample** in the **reservoir** based on the probability $\displaystyle \frac{1}{n}$.  

We can prove by **mathematical Induction** that at any point, after processing 
n **samples**, each **sample** from the **stream** has an equal probability $\displaystyle \frac{1}{n}$ of being included in the final **reservoir**.  

## References  

\[Wyman 2023\] [Chris Wyman, Markus Kettunen, Daqi Lin, Benedikt Bitterli, Cem Yuksel, Wojciech Jarosz, Pawel Kozlowski, Giovanni Francesco. "A Gentle Introduction to ReSTIR: Path Reuse in Real-time." SIGGRAPH 2023.](https://intro-to-restir.cwyman.org/)  
