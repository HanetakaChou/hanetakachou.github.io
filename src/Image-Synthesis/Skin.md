## Outline
FaceWorks | Disney SSS  | Separable SSS  
:-: | :-: | :-:  
Subsurface Scattering | investigating |  Blur
Deep Scatter | investigating |  Transmittance

## 1\.FaceWorks - NVIDIA

### Subsurface Scattering
The "Subsurface Scattering" of FaceWorks is based on \[Penner 2011\].  

The main idea is that the diffuse [BSDF](https://www.pbr-book.org/3ed-2018/Color_and_Radiometry/Surface_Reflection) is calculated by "D(θ,r)".  
The "θ" is merely the traditional "dot(N,L)", and the "r" is called "curvature" by \[Penner 2011\] which can be calculated on-the-fly as "r = ddx(p)/ddx(N)".  
Thus, the BSDF can be calculated as "BSDF(p,N,L) = D(dot(N,L), ddx(p)/ddx(N))".

However, the curvature is precomputed in FaceWorks. Perhaps the "on-the-fly" method is not efficient or not accurate.

And the "D(θ,r)" is "Pre-Integrated" and stored into a LUT(Look Up Texture) as the name of the paper suggests.

Unfortunately, the formula of "D(θ,r)" provided by "Chapter 1. Pre-Integrated Skin Shading" of "Part II. Rendering" of "GPU Pro 2" is NOT correct.  
Here is a page from [Zhihu (in Chinese)](https://zhuanlan.zhihu.com/p/56052015) which elaborates the derivation of the "$\displaystyle \operatorname{D}(\theta, r)$".  
Since the denominator of $\displaystyle \operatorname{D}(\theta, r) = \frac{\int_{-\frac{\pi}{2}}^{\frac{\pi}{2}} \cos (\theta + x) \cdot R(2r\sin(\frac{x}{2})) \,dx}{\int_{-\frac{\pi}{2}}^{\frac{\pi}{2}} R(2r\sin(\frac{x}{2})) \,dx}$ is a constant, the formula can be rewritten as $\displaystyle \operatorname{D}(\theta, r) = \int_{-\frac{\pi}{2}}^{\frac{\pi}{2}} \cos (\theta + x) \cdot \frac{R(2r\sin(\frac{x}{2}))}{\int_{-\frac{\pi}{2}}^{\frac{\pi}{2}} R(2r\sin(\frac{y}{2})) \,dy} \,dx$ (We use "y" to emphasize that this variable is different from x).  
Let $\displaystyle \operatorname{t}(x) = \frac{R(2r\sin(\frac{x}{2}))}{\int_{-\frac{\pi}{2}}^{\frac{\pi}{2}} R(2r\sin(\frac{y}{2})) \,dy}$, the key point is that t(x) obeys the formula "$\displaystyle \int_{-\frac{\pi}{2}}^{\frac{\pi}{2}} \operatorname{t}(x) \,dx = 1$" which indicates the energy conservation.


### Deep Scatter
The "Deep Scatter" of FaceWorks is based on the "16.3 Simulating Absorption Using Depth Maps" of \[Green 2004\].

## References
### 1\.FaceWorks - NVIDIA  
[NVIDIAGameWorks FaceWorks Github](https://github.com/NVIDIAGameWorks/FaceWorks/blob/master/doc/slides/FaceWorks-Overview-GTC14.pdf)  
\[Penner 2011\] [Eric Penner. "Pre-Integrated Skin Shading." SIGGRAPH 2011.](http://advances.realtimerendering.com/s2011/)  
\[Green 2004\] [Simon Green. "Chapter 16. Real-Time Approximations to Subsurface Scattering." GPU Gems 1.](https://developer.nvidia.com/gpugems/gpugems/part-iii-materials/chapter-16-real-time-approximations-subsurface-scattering)

### 2\.Disney SSS - Unity  
[Unity-Technologies Graphics Github ](https://github.com/Unity-Technologies/Graphics/blob/master/com.unity.render-pipelines.high-definition/Runtime/Material/SubsurfaceScattering/SubsurfaceScattering.hlsl)  
[Approximate Reflectance Profiles for Efficient Subsurface Scattering](https://graphics.pixar.com/library/)  
[Sampling Burley's Normalized Diffusion Profiles](https://zero-radiance.github.io/post/sampling-diffusion/)  

### 3\.Separable SSS - UE4  
[EpicGames UnrealEngine Github](https://github.com/EpicGames/UnrealEngine/blob/release/Engine/Shaders/Private/SeparableSSS.ush)  
[Separable Subsurface Scattering](http://www.iryoku.com/separable-sss/)  

### 4\.PBRT  
[Separable BSSRDFs](https://www.pbr-book.org/3ed-2018/Volume_Scattering/The_BSSRDF#SeparableBSSRDFs)  
// The meaning of this "Separable" seems different from the "Separable SSS"  //investigating more