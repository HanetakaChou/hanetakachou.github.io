# RTAO (Ray Traced Ambient Occlusion)  

By "Equation \(11.8\)" of [Real-Time Rendering Fourth Edition](https://www.realtimerendering.com/), the ambient occlusion can be calculated as $\displaystyle \operatorname{k_A}(\overrightarrow{p}) = \int_{\operatorname{H^2}(\overrightarrow{n})} \operatorname{V}(\overrightarrow{p}, \overrightarrow{\omega_i}) \frac{1}{\pi} (\cos \theta_i)^+ \, d \overrightarrow{\omega_i}$ where $\displaystyle \operatorname{V}$ is the visibility function and $\displaystyle \frac{1}{\pi} (\cos \theta_i)^+$ is the normalized clamped cosine.  

The main idea of RTAO is to use the Monte Carlo method to integrate the ambient occlusion in real time. The ambient occlusion is calculated by [AOIntegrator::Li](https://github.com/mmp/pbrt-v3/blob/master/src/integrators/ao.cpp) in PBRT-V3 and [AOIntegrator::Li](https://github.com/mmp/pbrt-v4/blob/ci/src/pbrt/cpu/integrators.cpp#L1414) by PBRT-V4.  

## 1\. Monte Carlo Integration  

### 1-1\. PDF  

Since $\displaystyle \int_{\operatorname{H^2}(\overrightarrow{n})} \frac{1}{\pi} (\cos \theta_i)^+ \, d \overrightarrow{\omega_i} = 1$, the normalized clamped cosine $\displaystyle \frac{1}{\pi} (\cos \theta_i)^+$ can be used as the PDF.  

### 1-2\. Estimator  

By "Equation (13.3)" of [PBR Book V3](https://pbr-book.org/3ed-2018/Monte_Carlo_Integration/The_Monte_Carlo_Estimator) and "Equation (2.7)" of [PBR Book V4](https://www.pbr-book.org/4ed/Monte_Carlo_Integration/Monte_Carlo_Basics#TheMonteCarloEstimator), we have the Monte Carlo estimator $\displaystyle \operatorname{k_A}(\overrightarrow{p}) = \int_{\operatorname{H^2}(\overrightarrow{n})} \operatorname{V}(\overrightarrow{p}, \overrightarrow{\omega_i}) \frac{1}{\pi} (\cos \theta_i)^+ \, d \overrightarrow{\omega_i} = \sum \frac{1}{N} \frac{\operatorname{V}(\overrightarrow{p}, \overrightarrow{\omega_i}) \frac{1}{\pi} (\cos \theta_i)^+}{\frac{1}{\pi} (\cos \theta_i)^+} = \sum \frac{1}{N} \operatorname{V}(\overrightarrow{p}, \overrightarrow{\omega_i})$.  

### 1-3\. Sampling Normalized Clamped Cosine  

By "13.6.3 Cosine-Weighted Hemisphere Sampling" of [PBR Book V3](https://www.pbr-book.org/3ed-2018/Monte_Carlo_Integration/2D_Sampling_with_Multidimensional_Transformations#Cosine-WeightedHemisphereSampling) and "A.5.3 Cosine-Weighted Hemisphere Sampling" of [PBR Book V4](https://www.pbr-book.org/4ed/Sampling_Algorithms/Sampling_Multidimensional_Functions#Cosine-WeightedHemisphereSampling), we can efficiently sample the normalized clamped cosine.  

### 1-4\. Low Discrepancy Sequence
  
By "20.3 Quasirandom Low-Discrepancy Sequences" of \[Colbert 2007\], "13.8.2 Quasi Monte Carlo" of [PBR Book V3](https://pbr-book.org/3ed-2018/Monte_Carlo_Integration/Careful_Sample_Placement#QuasiMonteCarlo) and "8.2.2 Low Discrepancy and Quasi Monte Carlo" of [PBR Book V4](https://pbr-book.org/4ed/Sampling_and_Reconstruction/Sampling_and_Integration#LowDiscrepancyandQuasiMonteCarlo), the **low discrepancy sequence** is the better alternative than **pseudo random sequence** to generate the $\displaystyle \xi_1$ and $\displaystyle \xi_2$.  

By "7.4.1 Hammersley and Halton Sequences" of [PBR Book V3](https://pbr-book.org/3ed-2018/Sampling_and_Reconstruction/The_Halton_Sampler#HammersleyandHaltonSequences) and "8.6.1 Hammersley and Halton Points" of [PBR Book V4](https://pbr-book.org/4ed/Sampling_and_Reconstruction/Halton_Sampler#HammersleyandHaltonPoints), the **Hammersley sequence** is a typical **low-discrepancy sequence**.  

The **Hammersley sequence** is calculated by [Hammersley](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/MonteCarlo.ush#L34) in UE4 and [Hammersley2d](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.core/ShaderLibrary/Sampling/Hammersley.hlsl#L415) in Unity3D.  

## 2\. Offset Ray Origin   

// TODO  
https://pbr-book.org/3ed-2018/Shapes/Managing_Rounding_Error  
https://pbr-book.org/4ed/Shapes/Managing_Rounding_Error  
Ray Tracing Gems Chapter 6  
   
## References  
\[Colbert 2007\] [Mark Colbert, Jaroslav Krivanek. "GPU-Based Importance Sampling." GPU Gems 3.](https://developer.nvidia.com/gpugems/gpugems3/part-iii-rendering/chapter-20-gpu-based-importance-sampling)  

