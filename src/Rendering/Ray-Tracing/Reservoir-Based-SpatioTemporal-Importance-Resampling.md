
# ReSTIR (Reservoir-Based SpatioTemporal Importance Resampling)  


## The Monte Carlo Estimator

["2.1.3 The Monte Carlo Estimator"](https://pbr-book.org/4ed/Monte_Carlo_Integration/Monte_Carlo_Basics#TheMonteCarloEstimator) of "PBR Book V4"  
["13.2 The Monte Carlo Estimator"](https://www.pbr-book.org/3ed-2018/Monte_Carlo_Integration/The_Monte_Carlo_Estimator#) of "PBR Book V3"  
"The only limitation on p(x) is that it must be nonzero for all x where | f(x) | > 0 (namely f(x) \ne 0)"  // actually // otherwise the estimator will NOT be unbiased  

$\displaystyle \mathop{\mathrm{E}} \left[ \frac{1}{N} \sum_{i = 1}^N \frac{\mathop{\mathrm{f}} (X_i)}{\mathop{\mathrm{p}} (X_i)} \right] = \frac{1}{N} \sum_{i = 1}^N \mathop{\mathrm{E}} \left[ \frac{\mathop{\mathrm{f}} (X_i)}{\mathop{\mathrm{p}} (X_i)} \right]$  
when p(x) \ne 0 for all x where f(x) \ne 0, we have $\displaystyle \mathop{\mathrm{E}} \left[ \frac{\mathop{\mathrm{f}} (X_i)}{\mathop{\mathrm{p}} (X_i)} \right] = \int \frac{\mathop{\mathrm{f}} (x)}{\mathop{\mathrm{p}} (x)} \mathop{\mathrm{p}} (x) dx = \int \mathop{\mathrm{f}} (x) dx$  

\[Wyman 2023\] supports  
\mathop{\mathrm{supp}}(f) // set of all x where f(x) \ne 0  
\mathop{\mathrm{supp}}(X) // set of all values x it can take with p(x) > 0 // namely p(x) \ne 0 // p(x) can Not < 0  
\mathop{\mathrm{supp}}(X) \subset \mathop{\mathrm{supp}}(f) // to be unbiased  

## Importance Sampling

["2.2.2 Importance Sampling"](https://pbr-book.org/4ed/Monte_Carlo_Integration/Improving_Efficiency#ImportanceSampling) of "PBR Book V4"  
[13.10 Importance Sampling](https://www.pbr-book.org/3ed-2018/Monte_Carlo_Integration/Importance_Sampling) of "PBR Book V3"  
when PDF proportional to f(x) \propt // variance zero // we can use only one sample // called "perfect important sampling"  

![](Reservoir-Based-SpatioTemporal-Importance-Resampling-Importance-Sampling.png)  

## MIS (Multiple Importance Sampling)

["13.10.1 Multiple Importance Sampling"](https://www.pbr-book.org/3ed-2018/Monte_Carlo_Integration/Importance_Sampling#MultipleImportanceSampling) of "PBR Book V3"  
["2.2.3 Multiple Importance Sampling"](https://pbr-book.org/4ed/Monte_Carlo_Integration/Improving_Efficiency#MultipleImportanceSampling) of "PBR Book V4"  

// example // balance heuristic  

// balance heuristic // one pdf = 0 // not all pdf = 0 // weight not zero  

// the domain one pdf not cover f(x) will not be detrimental  

// the union of the domains of all pdfs cover f(x) // enough 

![](Reservoir-Based-SpatioTemporal-Importance-Resampling-Multiple-Importance-Sampling.png)  


// TODO: \sum \mathop\mathrm w (x) = 1 // across all proposal distributions not all sample  
// Perhaps not necessary to be unbiased  

// TODO: \mathop\mathrm w_i = 0 when \mathop\mathrm p_k (x) = 0 for all k proposal distributions  // but actually such sample x will not be generated  

## Reservoir Sampling  

### Basic Reservoir Sampling  

By ["A.2 Reservoir Sampling"](https://www.pbr-book.org/4ed/Sampling_Algorithms/Reservoir_Sampling#) of "PBR Book V4", we have the **basic reservoir sampling**.  
   
We sequentially process each **sample** from the **stream**. The total length of the **stream** can indeed be infinite which is too large to be stored in the memory.   

We assume that we have processed **n** **samples**. This means that the number of the **seen samples** is **n**. For the **basic reservoir sampling**, the **reservoir** can hold at most **1** **reservoir sample**, and the first **1** **seen** **sample** is always selected to initialize the **reservoir**. For each subsequent **seen** **candidate sample**, we have the probability $\displaystyle \frac{1}{n}$ of selecting it to replace the existing **sample** within the **reservoir**.  

We can prove by **mathematical Induction** that at any iteration, when we have processed n **samples**, each **sample** from the **stream** has the equal probability $\displaystyle \frac{1}{n}$ of being included in the final **reservoir**.  

> Base Case  
>>
>> At the iteration, when we have processed n = 1 **sample**, each **sample** has the equal probability $\displaystyle \frac{1}{1} = 1$ of being included in the final **reservoir**.  
>  
> Inductive Step  
>> 
>> We assume that at the iteration, when we have processed n = k **samples**, each **sample** from the **stream** has the equal probability $\displaystyle \frac{1}{k}$ of being included in the final **reservoir**.  
>>   
>> And we would like to prove that at the iteration, when we have processed n = k + 1 **samples**, each **sample** from the **stream** has the equal probability $\displaystyle \frac{1}{k + 1}$ of being included in the final **reservoir**.  
>>  
>> Evidently, the (k + 1)-th **seen sample** has the probability $\displaystyle \frac{1}{k + 1}$ of being selected to replace the existing **sample** within the **reservoir** and thus being included in the final **reservoir**.  
>>  
>> For the previous k **seen samples**, they have the probability $\displaystyle \frac{1}{k}$ of being included in the final **reservoir** at k-th iteration. At the same time, they have the probability $\displaystyle 1 - \frac{1}{k + 1} = \frac{k}{k + 1}$ of NOT being replaced by the (k + 1)-th **seen sample** at (k + 1)-th iteration. This means that they have the probability $\displaystyle \frac{1}{k} \times \frac{k}{k + 1} = \frac{1}{k + 1}$ of being included in the final **reservoir** at (k + 1)-th iteration.  


## RIS (Resampled Importance Sampling)

\[Wyman 2023\]  

generate M samples as per PDF p(x)  
choose one sample X_i from these M samples proportional to w_i // P = \frac{w_i}{\sum_n=1^M w_n}   
W_X unbiased contribution weight (estimate of (\frac{1}{M} f(x)?) 1/p(x)) // I = f(X) W_x = \frac{1}{M} f(x) \frac{1}{\mathop{\mathrm{p}}(x)}  
// target function: \mathop{\mathrm{\hat{p}}}(X)  
w_i = \frac{1}{M} \frac{\mathop{\mathrm{\hat{p}}}(X_i)}{\mathop{\mathrm{p}}(X_i)}  
W_X = \frac{1}{\mathop{\mathrm{\hat{p}}}(X)} \sum_{i=1}^M w_i  
// out PDF is p(X) = \frac{\mathop{\mathrm{\hat{p}}}(X)}{\int \mathop{\mathrm{\hat{p}}}(X)}   
// target function = f(x) // output PDF approaches perfect importance samping   
// not practical // we should use calculate integral first to generate M samples as per the PDF  
// approximate perfect importance samping  

## SpatioTemporal Reuse  


## References  

\[Wyman 2023\] [Chris Wyman, Markus Kettunen, Daqi Lin, Benedikt Bitterli, Cem Yuksel, Wojciech Jarosz, Pawel Kozlowski, Giovanni Francesco. "A Gentle Introduction to ReSTIR: Path Reuse in Real-time." SIGGRAPH 2023.](https://intro-to-restir.cwyman.org/)  
