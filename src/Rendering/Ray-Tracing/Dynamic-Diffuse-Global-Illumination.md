# DDGI (Dynamic Diffuse Global Illumination)  

https://github.com/NVIDIAGameWorks/RTXGI-DDGI  

https://morgan3d.github.io/articles/2019-04-01-ddgi/index.html  

Dynamic Diffuse Global Illumination with Ray-Traced Irradiance Fields  

Real-Time Global Illumination using Precomputed Light Field Probes  

## Avoid Leaks  

The **visibility** information is the most important difference between **DDGI** and traditional **irradiance environment mapping**. The Ray Tracing APIs, such as [DXR (DirectX Raytracing)](https://microsoft.github.io/DirectX-Specs/d3d/Raytracing.html) and [Vulkan Ray Tracing](https://www.khronos.org/blog/ray-tracing-in-vulkan), make it possible to calculate the hit distance in hundreds of directions at each **light probe** position in real time.  

Analogous to the **VSM (Variance Shader Map)**, the **Chebyshev's inequality** is used to compare the distance of the shading position with the "average" distance stored in the light probe to test the **visibility**.  

TODO: According to the **VSM (Variance Shader Map)**, both the distance and the **squared** distance should be stored in the light probe. However, according to the [DDGIGetVolumeIrradiance](https://github.com/NVIDIAGameWorks/RTXGI-DDGI/blob/main/rtxgi-sdk/shaders/ddgi/Irradiance.hlsl#L65) of the **RTXGI SDK**, only the distance is stored in the light probe and the **squared** distance is calculated from the **sampled** distance. This may cause the "average" **squared** distance incorrect.  
