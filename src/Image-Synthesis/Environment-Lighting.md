## Environment Lighting

The name **environment lighting** is from "10.2 Environment Lighting" of [Real-Time Rendering Fourth Edition](https://www.realtimerendering.com/). The most important difference between environment light and global illumination is that the shading algorithm of the environment light does NOT depend on the information about other positions on the surface than the shading position.  


### Irradiance Environment Lighting  

Let $\displaystyle \operatorname{L}(\omega)$ denote the infinitely distant radiance distribution. By \[Ramamoorthi 2001\], the irradiance can be calculated as $\displaystyle E(\overrightarrow{n}) = \int_{\operatorname{\Omega}(\overrightarrow{n})} \operatorname{L}(\omega) |\cos \theta| \, d \omega = \int_{\operatorname{\Omega}(\overrightarrow{n})} \operatorname{L}(\omega) |\overrightarrow{n} \cdot \overrightarrow{\omega}| \, d \omega$.  





```
diffuseConvolution(outputEnvironmentMap, inputEnvironmentMap)
{
    for_all{T0 : outputEnvironmentMap}
    {
        sum = 0;
        N = envMap_direction(T0);
        for_all{T1 : inputEnvironmentMap}
        {
            L = envMap_direction(T1);
            I = inputEnvironmentMap[T1];
            sum += max(0, dot(L, N)) * I; // where is 'dω'?
        }
        T0 = sum;
    }
    return outputEnvironmentMap;
}
```

```
float2 map_to_tile_and_offset(tile, offsetTexCoord)
{
    return (tile / numTiles) + (offsetTexCoord / (numTiles * numSamples));
}

float3 SH_Projection(inputEnvironmentMap, dω_Ylm, current_Llm : VPOS) : COLOR
{
    sum = 0;
    for_all{T0 : inputEnvironmentMap}
    {
        T1 = map_to_tile_and_offset(current_Llm, T0);
        weighted_SHbasis = dω_Ylm[T1];
        radiance_Sample = inputEnvironmentMap[T0];
        sum += radiance_Sample * weighted_SHbasis;
    }
    return sum;
}

float3 SH_Evaluation(L_lm, Alm_Ylm, thetaPhi : VPOS) : COLOR
{
    sum = 0;
    for_all{T0 : Llm}
    {
        T1 = map_to_tile_and_offset(T0, thetaPhi);
        weighted_BRDF = Alm_Ylm[T1];
        light_environment = inputEnvironmentMap[T0];
        sum += light_environment * weighted_BRDF;
        return sum;
    }
}
```


## References 
\[Ramamoorthi 2001\] [Ravi Ramamoorthi, Pat Hanrahan. "An Efficient Representation for Irradiance Environment Maps." SIGGRAPH 2001.](https://graphics.stanford.edu/papers/envmap/)
\[King 2005\] [Gary King. "Real-Time Computation of Dynamic Irradiance Environment Maps." GPU Gems 2.](https://developer.nvidia.com/gpugems/gpugems2/part-ii-shading-lighting-and-shadows/chapter-10-real-time-computation-dynamic)  
\[Colbert 2007\] [Mark Colbert, Jaroslav Krivanek. "GPU-Based Importance Sampling." GPU Gems 3.](https://developer.nvidia.com/gpugems/gpugems3/part-iii-rendering/chapter-20-gpu-based-importance-sampling)  