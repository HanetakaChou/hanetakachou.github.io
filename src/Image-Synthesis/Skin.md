## Outline
FaceWorks - NVIDIA | Disney SSS - Unity | Separable SSS - UE4  
:-: | :-: | :-:  
Subsurface Scattering | investigating |  Blur
Deep Scatter | investigating |  Transmittance

### Diffusion Profile  

Currently, all real time methods are based on the diffusion profile("14.4.2 Rendering with Diffusion Profile" of [dEon 2007]) rather than the [BSSRDF](https://www.pbr-book.org/3ed-2018/Color_and_Radiometry/Surface_Reflection#TheBSSRDF).  

The subsurface scattering is simulated by a much simpler process that the light of each location is scattered to the vicinal locations according to the weights indicated by the diffusion profile.  

Evidently, an equivalent gather operation can be used to replace the scatter operation, and the diffuse term can be considered as "$\displaystyle \operatorname{L}_o(p_o) = \int_A \operatorname{R}(p_o, p_i) \cdot \operatorname{BRDF}(p_i, w_i) \cdot \operatorname{L_i}(p_i, w_i) \cdot |\cos(\theta)| \, dA$" where the "$\displaystyle \operatorname{R}(p_o, p_i)$" is the diffusion profile, and the $\displaystyle w_o$ is deliberately omitted since the diffuse term is irrelevant to the $\displaystyle w_o$.  

Currently, all real time methods assume a homogeneous material, and the $\displaystyle \operatorname{R}(p_o, p_i)$ can be considered radially symmetric, namely, $\displaystyle \operatorname{R}(\operatorname{distance}(p_o, p_i))$. And the diffuse term can be simplified to "$\displaystyle \operatorname{L}_o(p_o) = \int_A \operatorname{R}(\operatorname{distance}(p_o, p_i)) \cdot \operatorname{BRDF}(p_i, w_i) \cdot \operatorname{L_i}(p_i, w_i) \cdot |\cos(\theta)| \, dA$".

However, although the method based on the diffusion profile is much simpler than the BSSRDF, a trivial one pass 2D convolution is still too expensive for real time rendering. Actually, if the width of the efficient domain of the diffusion profile is about 16 mm, and the width of pixel is about 0.25 mm, we would need a 4096(64 x 64) tap blur shader. Thus, a more efficient method needs to be proposed.

## 1\. FaceWorks - NVIDIA

### 1-1\. Subsurface Scattering
The "Subsurface Scattering" of FaceWorks is based on \[Penner 2011\], and the related source code in FaceWorks is the "EvaluateSSSDiffuseLight" function in "[lighting.hlsli](https://github.com/NVIDIAGameWorks/FaceWorks/blob/master/samples/d3d11/shaders/lighting.hlsli)".  

The main idea of \[Penner 2011\] is that the "$\displaystyle \operatorname{BRDF}(p_i, w_i)$" is assumed to be the constant "$\displaystyle \operatorname{BRDF}(p_o, w_i)$" for all vicinal locations.  

And thus, the "$\displaystyle \operatorname{R}(\operatorname{distance}(p_o, p_i)) \cdot |\cos(\theta)|$" part of the diffuse term can be "Pre-Integrated" and stored in a LUT(Look Up Texture) which is called the "$\displaystyle \operatorname{D}(\theta, \frac{1}{r})$".   

The "θ" is merely the traditional "dot(N,L)", and the "$\displaystyle \frac{1}{r}$", which is called "curvature" by \[Penner 2011\], can be calculated on-the-fly as "$\displaystyle \frac{1}{r} = \frac{\operatorname{ddx}(N)}{\operatorname{ddx}(P)}$". However, the "on-the-fly" method may be inaccurate since FaceWorks chooses to precompute the curvature instead.  

In conclusion, the diffuse term can be calculated as "$\displaystyle \operatorname{D}(\operatorname{dot}(N,L), \frac{\operatorname{ddx}(N)}{\operatorname{ddx}(P)}) \cdot \operatorname{BRDF}(P) \cdot LI$".
 
Usually, the diffusion profile is normalized which indicates the energy conservation. This means that $\displaystyle \int_0^\infin R(r) \, dr =1$.  

However, according to \[Penner 2011\], $\displaystyle \operatorname{D}(\theta, \frac{1}{r}) = \frac{\int_{-\frac{\pi}{2}}^{\frac{\pi}{2}} | \cos (\theta + x) | \cdot R(2r\sin(\frac{x}{2})) \,dx}{\int_{-\frac{\pi}{2}}^{\frac{\pi}{2}} R(2r\sin(\frac{y}{2})) \,dy}$. The denominator is added to make sure the diffusion profile is normalized.

// radially symmetric only calculate one direction and thus we need to divide to normalize //approximated a spherical integration with integration on a ring

// "GFSDK_FaceWorks_GenerateCurvatureLUT"
// 2rsin(x/2) replaced by rx("delta")  
// denominator is omitted // total diffuse reflectance

### 1-2\. Deep Scatter
The "Deep Scatter" of FaceWorks is based on the "16.3 Simulating Absorption Using Depth Maps" of \[Green 2004\].

## 2\. Disney SSS - Unity  
TODO

## 3\. Separable SSS - UE4  
TODO

Advantages of a Sum-of-Gaussians Diffusion Profile

However, each Gaussian convolution texture can be computed separably and, provided our fit is accurate, the weighted sum of these textures will accurately approximate the lengthy 2D convolution by the original, nonseparable function. This provides a nice way to accelerate general convolutions by nonseparable functions: approximate a nonseparable convolution with a sum of separable convolutions. We use this same idea to accelerate a high-dynamic-range (HDR) bloom filter in Section 14.6.


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