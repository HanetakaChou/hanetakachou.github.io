## Outline
FaceWorks - NVIDIA | Disney SSS - Unity | Separable SSS - UE4  
:-: | :-: | :-:  
Subsurface Scattering | investigating |  Blur
Deep Scatter | investigating |  Transmittance

### Diffusion Profile  

The current real time methods are all based on the diffusion profile("14.4.2 Rendering with Diffusion Profile" of [dEon 2007]) rather than the [BSSRDF](https://www.pbr-book.org/3ed-2018/Color_and_Radiometry/Surface_Reflection#TheBSSRDF).  
The subsurface scattering is simulated by a much simpler process that the light of each location is scattered to the vicinal locations based on the weight indicated by the diffusion profiles.  

## 1\. FaceWorks - NVIDIA

### 1-1\. Subsurface Scattering
The "Subsurface Scattering" of FaceWorks is based on \[Penner 2011\], and the related source code in FaceWorks is the "EvaluateSSSDiffuseLight" function in "[lighting.hlsli](https://github.com/NVIDIAGameWorks/FaceWorks/blob/master/samples/d3d11/shaders/lighting.hlsli)".  

According to \[Penner 2011\], an equivalent gather operation can be used to replace the scatter operation of [dEon 2007].  
And the diffuse term can be calculated as "$\displaystyle \operatorname{L}_o(p_o) = \int_A \operatorname{T}(\operatorname{distance}(p_o, p_i)) \cdot \operatorname{BRDF}(p_i, w_i) \cdot \operatorname{L_i}(p_i, w_i) \cdot |\cos(\theta)| \, dA$" where the $\displaystyle \operatorname{T}(d) = \frac{\operatorname{R}(d)}{\int_A \operatorname{R}(\operatorname{distance}(p_o, p_i)) \, dA}$, which is introduced for energy conservation, and the "$\displaystyle \operatorname{R}(d)$" is the diffusion profile. The $\displaystyle w_o$ in the formula is omitted because the diffuse term is irrelevant to the $\displaystyle w_o$.  

The main idea of \[Penner 2011\] is that the "$\displaystyle \operatorname{BRDF}(p_i, w_i)$" is assumed to be the constant "$\displaystyle \operatorname{BRDF}(p_o, w_i)$" for all vicinal locations.  
And thus, the "$\displaystyle \operatorname{T}(\operatorname{distance}(p_o, p_i)) \cdot |\cos(\theta)|$" part of the diffuse term can be "Pre-Integrated" and stored in a LUT(Look Up Texture) which is called the "D(θ,r)".   
The "θ" is merely the traditional "dot(N,L)", and the "r" is called "curvature" by \[Penner 2011\] which can be calculated on-the-fly as "$\displaystyle r = \frac{\operatorname{ddx}(P)}{\operatorname{ddx}(N)}$". However, the "on-the-fly" method may be inaccurate since FaceWorks chooses to precompute the curvature instead.  
In conclusion, the diffuse term can be calculated as "$\displaystyle \operatorname{D}(\operatorname{dot}(N,L), \frac{\operatorname{ddx}(P)}{\operatorname{ddx}(N)}) \cdot \operatorname{BRDF}(P) \cdot LI$".
 
There is a page from [Zhihu (in Chinese)](https://zhuanlan.zhihu.com/p/56052015) which elaborates the derivation of the "D(θ,r)".  
Since the denominator of $\displaystyle \operatorname{D}(\theta, r) = \frac{\int_{-\frac{\pi}{2}}^{\frac{\pi}{2}} \cos (\theta + x) \cdot R(2r\sin(\frac{x}{2})) \,dx}{\int_{-\frac{\pi}{2}}^{\frac{\pi}{2}} R(2r\sin(\frac{x}{2})) \,dx}$ is a constant, the formula can be rewritten as $\displaystyle \operatorname{D}(\theta, r) = \int_{-\frac{\pi}{2}}^{\frac{\pi}{2}} \cos (\theta + x) \cdot \frac{R(2r\sin(\frac{x}{2}))}{\int_{-\frac{\pi}{2}}^{\frac{\pi}{2}} R(2r\sin(\frac{y}{2})) \,dy} \,dx$ (We use "y" to emphasize that this variable is irrelevant to x).  
Let $\displaystyle \operatorname{T}(x) = \frac{R(2r\sin(\frac{x}{2}))}{\int_{-\frac{\pi}{2}}^{\frac{\pi}{2}} R(2r\sin(\frac{y}{2})) \,dy}$, the key point is that the T(x) obeys the formula "$\displaystyle \int_{-\frac{\pi}{2}}^{\frac{\pi}{2}} \operatorname{T}(x) \,dx = 1$" which indicates the energy conservation.

### 1-2\. Deep Scatter
The "Deep Scatter" of FaceWorks is based on the "16.3 Simulating Absorption Using Depth Maps" of \[Green 2004\].

## 2\. Disney SSS - Unity  
TODO

## 3\. Separable SSS - UE4  
TODO

## References
[dEon 2007] [Eugene dEon, David Luebke. "Advanced Techniques for Realistic Real-Time Skin Rendering." GPU Gem 3.](https://developer.nvidia.com/gpugems/gpugems3/part-iii-rendering/chapter-14-advanced-techniques-realistic-real-time-skin)  


### FaceWorks - NVIDIA  
[NVIDIAGameWorks FaceWorks Github](https://github.com/NVIDIAGameWorks/FaceWorks/blob/master/doc/slides/FaceWorks-Overview-GTC14.pdf)  
\[Penner 2011\] [Eric Penner. "Pre-Integrated Skin Shading." SIGGRAPH 2011.](http://advances.realtimerendering.com/s2011/)  
\[Green 2004\] [Simon Green. "Chapter 16. Real-Time Approximations to Subsurface Scattering." GPU Gems 1.](https://developer.nvidia.com/gpugems/gpugems/part-iii-materials/chapter-16-real-time-approximations-subsurface-scattering)

### Disney SSS - Unity  
[Unity-Technologies Graphics Github ](https://github.com/Unity-Technologies/Graphics/blob/master/com.unity.render-pipelines.high-definition/Runtime/Material/SubsurfaceScattering/SubsurfaceScattering.hlsl)  
[Approximate Reflectance Profiles for Efficient Subsurface Scattering](https://graphics.pixar.com/library/)  
[Sampling Burley's Normalized Diffusion Profiles](https://zero-radiance.github.io/post/sampling-diffusion/)  

### Separable SSS - UE4  
[EpicGames UnrealEngine Github](https://github.com/EpicGames/UnrealEngine/blob/release/Engine/Shaders/Private/SeparableSSS.ush)  
[Jimenez 2015] [Jorge Jimenez, Karoly Zsolnai, Adrian Jarabo1, Christian Freude, Thomas Auzinger, Xian-Chun Wu, Javier von der Pahlen, Michael Wimmer and Diego Gutierrez. "Separable Subsurface Scattering." EGSR 2015.](http://www.iryoku.com/separable-sss/)  

### PBRT  
[Separable BSSRDFs](https://www.pbr-book.org/3ed-2018/Volume_Scattering/The_BSSRDF#SeparableBSSRDFs)  
// The meaning of this "Separable" seems different from the "Separable SSS"  //investigating more