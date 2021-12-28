## Outline
N/A| [FaceWorks - NVIDIA](https://github.com/NVIDIAGameWorks/FaceWorks/blob/master/doc/slides/FaceWorks-Overview-GTC14.pdf) | [Separable SSS - UE4](https://github.com/EpicGames/UnrealEngine/blob/release/Engine/Shaders/Private/SeparableSSS.ush) | [Disney SSS - Unity3D](https://github.com/Unity-Technologies/Graphics/blob/master/com.unity.render-pipelines.high-definition/Runtime/Material/SubsurfaceScattering/SubsurfaceScattering.hlsl) 
:-: | :-: | :-: | :-:  
Subsurface Scattering | Pre-Integrated | Blur |  TODO
Transmitted Light | Deep Scatter | Transmittance |  TODO

### Diffusion Profile  

Currently, all real time approaches are based on the diffusion profile("14.4.2 Rendering with Diffusion Profile" of \[dEon 2007\]) rather than the [BSSRDF](https://www.pbr-book.org/3ed-2018/Color_and_Radiometry/Surface_Reflection#TheBSSRDF).  

By using the diffusion profile, the subsurface scattering, which was described by the BSSRDF, is simplified by scattering the **amount of light** (technically, the **irradiance E**) of each location to the vicinal locations according to the weights indicated by the diffusion profile.  

Note that the **outgoing** irradiance E can also be called **radiant exitance M** and might be called **radiosity B** in the last century. 

In real time rendering, the light is assumed to be the punctual light rather than the area light.  

The [Delta Distribution](https://www.pbr-book.org/3ed-2018/Light_Transport_I_Surface_Reflection/Sampling_Light_Sources#LightswithSingularities) is applied, and the reflectance equation is simplified to $\displaystyle \operatorname{L}_o(p, \omega_o) = \int_\Omega \operatorname{BRDF}(p, \omega_o, \omega_i) \cdot \operatorname{L_i}(p, \omega_i) \cdot |\cos(\theta_i)| \, d\omega_i = \operatorname{BRDF}(p_i, \omega_o, \omega_i) \otimes \operatorname{E_{L}}(p) \otimes |\cos(\theta_i)|$ where the $\displaystyle \operatorname{E_{L}}(p)$ is the irradiance perpendicular to the light direction.   

And since the diffuse BRDF equals $\displaystyle \frac{c_{diffuse}}{\pi}$ which is irrelevant to the the $\displaystyle w_o$ and the $\displaystyle w_i$, the reflectance equation can be simplified further to $\displaystyle \operatorname{L}_o(p) = \frac{\operatorname{c_{diffuse}}(p)}{\pi} \otimes \operatorname{E_{L}}(p) \otimes |\cos(\theta_i)|$.  

Thus, the irradiance E and the radiant exitance M can be calculated as $\displaystyle \operatorname{E}(p) = \operatorname{M}(p) = \int_\Omega \operatorname{L}_o(p, \omega_o) \, d\omega_o  = \operatorname{L}_o(p) \cdot \int_\Omega 1 \, d\omega_o = \operatorname{L}_o(p) \cdot \pi = \operatorname{c_{diffuse}}(p) \otimes \operatorname{E_{L}}(p) \otimes |\cos(\theta_i)|$. 

Evidently, an equivalent gather operation can be used to replace the scatter operation, and the total radiant exitance can be considered as $\displaystyle \operatorname{M}(p_o) = \int_{S_{p_i}} \operatorname{R}(p_o, p_i) \cdot \operatorname{E}(p_i) \, dp_i$ where the $\displaystyle \operatorname{R}(p_o, p_i)$ is the diffusion profile.  

And, currently, all real time approaches assume that the material is homogeneous. This means that the $\displaystyle \operatorname{R}(p_o, p_i)$ is radially symmetric, and can be characterized by $\displaystyle \operatorname{R}(\operatorname{distance}(p_o, p_i))$.  

And since for the diffuse term, the outgoing radiance is assumed to be the same in all directions, the diffuse term is simplified to $\displaystyle \operatorname{L}_o(p_o) = \frac{\operatorname{M}(p_o)}{\pi} = \frac{1}{\pi} \cdot \int_{S_{p_i}} \operatorname{R}(\operatorname{distance}(p_o, p_i)) \cdot \operatorname{c_{diffuse}}(p_i) \cdot \operatorname{E_{L}}(p_i) \cdot |\cos(\theta_i)| \, dp_i$.  

However, although the proposals based on the diffusion profile are much simpler than the BSSRDF, a general 2D convolution is still too expensive for real time rendering. Actually, according to \[dEon 2007\], if the width of the significant contribution domain of the diffusion profile is about 16 mm, and the width of pixel is about 0.25 mm, we would sample 4096(64 x 64) pixels in the shader. Thus, we have to propose more efficient approaches.

## 1\. FaceWorks - NVIDIA

### 1-1\. Pre-Integrated
The **Subsurface Scattering** of FaceWorks is based on the **Pre-Integrated** \[Penner 2011\], and the related source code in FaceWorks is the **EvaluateSSSDiffuseLight** function in [lighting.hlsli](https://github.com/NVIDIAGameWorks/FaceWorks/blob/master/samples/d3d11/shaders/lighting.hlsli).  

The main idea of \[Penner 2011\] is that the $\displaystyle \operatorname{c_{diffuse}}(p_i)$ is assumed to be the constant $\displaystyle \operatorname{c_{diffuse}}(p_o)$ for all vicinal locations.  

And thus, the $\displaystyle \operatorname{R}(\operatorname{distance}(p_o, p_i)) \cdot |\cos(\theta_i)|$ part of the diffuse term can be **pre-integrated** and stored in a LUT(Look Up Texture) which is called the $\displaystyle \operatorname{D}(\theta, \frac{1}{r})$.   

The **θ** is merely the traditional **dot(N,L)**, and the $\displaystyle \frac{1}{r}$, which is called **curvature** by \[Penner 2011\], can be calculated on-the-fly as $\displaystyle \frac{1}{r} = \frac{\operatorname{ddx}(N)}{\operatorname{ddx}(P)}$. However, the on-the-fly method may be inaccurate since FaceWorks chooses to precompute the curvature instead.  

In conclusion, the diffuse term can be calculated as $\displaystyle \operatorname{D}(\operatorname{dot}(N,L), \frac{\operatorname{ddx}(N)}{\operatorname{ddx}(P)}) \otimes \frac{\operatorname{c_{diffuse}}(p)}{\pi} \otimes \operatorname{E_{L}}(p)$.
 
Usually, the diffusion profile is normalized which indicates the energy conservation. This means that $\displaystyle \int_0^\infin R(r) \, dr =1$.  

However, according to \[Penner 2011\], $\displaystyle \operatorname{D}(\theta, \frac{1}{r}) = \frac{\int_{-\pi}^{\pi} | \cos (\theta + x) | \cdot R(2r\sin(\frac{x}{2})) \,dx}{\int_{-\pi}^{\pi} R(2r\sin(\frac{y}{2})) \,dy}$. The denominator is added to make sure the diffusion profile is normalized.

In the GPU Pro 2, the $\displaystyle \operatorname{D}(\theta, \frac{1}{r})$ is calculated by **integrateDiffuseScatteringOnRing**. And there are some points to note.  
1. The **pre-integral** is performed on a ring rather than on a sphere. This is reasonable since it is assumed that the diffusion profile is radially symmetric.  
2. \[Penner 2011\] merely follows the \[dEon 2007\] and the diffusion profile is approximated by the Gaussians (the **Scatter** in the code).  
However, the motivation of \[dEon 2007\] is that the [Gaussian blur](https://en.wikipedia.org/wiki/Gaussian_blur) is a **separable filter**, and thus the general 2D convolution can be replaced by 1D convolutions.  
The approach proposed by \[Penner 2011\] **pre-integrates** the convolution, and it is acceptable to perform a general 2D convolution even by using the exact accurate diffusion profile since the efficiency doesn't matter too much for offline precomputing.  
3. In the FaceWorks, according to the **numerical quadrature**, the funtion value $\operatorname{f}(x)$ is multiplied by the difference of the domain $\displaystyle \operatorname{\Delta}x$ (the **scale** in the code).  
However, in the GPU Pro 2, there is no such code like **scale** since the $\displaystyle \operatorname{\Delta}x$ appears in both numerator and denominator, and the it is not necessary to multiply $\displaystyle \operatorname{f}(x)$ by $\displaystyle \operatorname{\Delta}x$.  

In the FaceWorks, the $\displaystyle \operatorname{D}(\theta, \frac{1}{r})$ is calculated by **GFSDK_FaceWorks_GenerateCurvatureLUT**. However, there is some subtle modification.  
1. The $\displaystyle 2r\sin(\frac{x}{2})$ is replaced by the $\displaystyle rx$ (the **delta** in the code). Technically, the $\displaystyle 2r\sin(\frac{x}{2})$ is more correct since the diffusion profile describes the light absorption inside the medium rather than over the surface. Perhaps the $\displaystyle 2r\sin(\frac{x}{2})$ and the $\displaystyle rx$ are close when the x is small.  
2. The denominator $\displaystyle \int_{-\pi}^{\pi} R(2r\sin(\frac{y}{2})) \,dy$ is omitted perhaps due to the fact that the diffusion profile has been normalized. Actually, I try to calculate the denominator by myself and I find the donominator is really close to one.  
3. In the GPU Pro 2, three normals should be used for different RGB components and the LUT should be sampled three times according to three different $\displaystyle \theta$s.  
Perhaps this method is not efficient and the FaceWorks detaches the $\displaystyle \operatorname{dot}(N,L)$, which denotes the part of the integral where x is close to zero and the diffuse profile is close to one, from the total integral $\displaystyle \operatorname{D}(\theta, \frac{1}{r})$. Evidently, the remaining part of the integral is relatively small, and thus FaceWorks maps the remaining part of the integral from [-0.25, 0.25] to [0, 1] to fully use the precision of the texture (the **rgbAdjust** in the code).  
The **GFSDK_FaceWorks_EvaluateSSSDirectLight** is used to calculate the diffuse term. The LUT is only sampled once and three normals are used to calculate the $\displaystyle \operatorname{dot}(N,L)$ which is detached from the total integral. 


### 1-2\. Deep Scatter
The **Transmitted Light** of FaceWorks is based on the **16.3 Simulating Absorption Using Depth Maps** of \[Green 2004\].  

TODO

## 2\. Separable SSS - UE4  

### 2-1\. Blur

The approach of \[dEon 2007\] is to approximate the diffusion profile by the weighted sum of 6 Gaussians, and thus the general 2D convolution can be replaced by 12(2 x 6) 1D convolutions since the [Gaussian blur](https://en.wikipedia.org/wiki/Gaussian_blur) is a **separable filter**.

And according to the **numerical quadrature**, the funtion value sampled from the irradiance texture should be multiplied by the difference of the domain $\displaystyle \operatorname{\Delta} p_i$. \[dEon 2007\] proposed the **stretch texture**, where the difference of the world position is stored, to described the $\displaystyle \operatorname{\Delta} p_i$.  

However, the approach proposed by \[dEon 2007\] is applied in texture space which is too weird according to the convention of the real time rendering. And the screen space approach is proposed by \[Jimenez 2009\] and \[Jimenez 2010\].  

Definitely, the screen space depth can be used to calculate the world position and thus the $\displaystyle \operatorname{\Delta} p_i$ can be obtained. However, the **stretch factor** proposed by \[Jimenez 2010\] is not proportional to the difference of the world position, and in my opinion, is empirical. And \[Mikkelsen 2010\] proposed a more reasonable approach which is based on the mathematical derivation.  

However, the approach proposed by \[Jimenez 2010\] still needs 2N passes to perform the 2N 1D convolutions where the N is the number of Gaussians. Evidently, this is still too expensive for real time rendering. And the 2 passes approach is proposed by \[Jimenez 2015\] by assuming the irradiance is [additively separable](https://calculus.subwiki.org/wiki/Additively_separable_function) and **pre-integrating** the **kernel**.  

Note that in image processing, the **filter** is a (continuous) function which is approximated by a discrete and finite **kernel**.  

Note that the $\displaystyle ||R_d||_1$ and $\displaystyle ||a_p||_1$denotes the [$\displaystyle L_p$ space](https://en.wikipedia.org/wiki/Lp_space). This means that $\displaystyle ||\operatorname{R_d}||_1 = ||\operatorname{a_p}||_1 = \int \operatorname{a_p}(x-u) \,du =  \int \operatorname{a_p}(y-v) \,dv$. The integral is performed on the whole domain of the diffusion profile and evidently the integral is irrelevant to x or y.  



### 2-2\. Transmittance

TODO

## 3\. Disney SSS - Unity3D  
TODO

## References

\[dEon 2007\] [Eugene dEon, David Luebke. "Advanced Techniques for Realistic Real-Time Skin Rendering." GPU Gem 3.](https://developer.nvidia.com/gpugems/gpugems3/part-iii-rendering/chapter-14-advanced-techniques-realistic-real-time-skin)  
\[NVIDIA 2014\] [NVIDIAGameWorks FaceWorks Github](https://github.com/NVIDIAGameWorks/FaceWorks/blob/master/doc/slides/FaceWorks-Overview-GTC14.pdf)  
\[Penner 2011\] Eric Penner, George Borshukov. "Pre-Integrated Skin Shading." GPU Pro 2.  
\[Penner 2011\] [Eric Penner. "Pre-Integrated Skin Shading." SIGGRAPH 2011.](http://advances.realtimerendering.com/s2011/)  
\[Green 2004\] [Simon Green. "Chapter 16. Real-Time Approximations to Subsurface Scattering." GPU Gems 1.](https://developer.nvidia.com/gpugems/gpugems/part-iii-materials/chapter-16-real-time-approximations-subsurface-scattering)  
\[Jimenez 2009\] [Jorge Jimenez, Veronica Sundstedt, Diego Gutierrez. "Screen-Space Perceptual Rendering of Human Skin." ACM TAP 2009](https://www.iryoku.com/sssss/)  
\[Jimenez 2010\] Jorge Jimenez, Diego Gutierrez. "Screen-Space Subsurface Scattering." GPU Pro 1.  
\[Mikkelsen 2010\] [Morten Mikkelsen. "Skin Rendering by Pseudo–Separable Cross Bilateral Filtering." Naughty Dog.](https://mmikk.github.io/papers3d/cbf_skin.pdf)  
\[Jimenez 2015\] [Jorge Jimenez, Karoly Zsolnai, Adrian Jarabo1, Christian Freude, Thomas Auzinger, Xian-Chun Wu, Javier von der Pahlen, Michael Wimmer and Diego Gutierrez. "Separable Subsurface Scattering." EGSR 2015.](http://www.iryoku.com/separable-sss/)  
