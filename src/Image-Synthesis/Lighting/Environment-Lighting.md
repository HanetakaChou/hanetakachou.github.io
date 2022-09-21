# Environment Lighting

The name **environment lighting** is from "10.2 Environment Lighting" of [Real-Time Rendering Fourth Edition](https://www.realtimerendering.com/). The most important difference between environment light and global illumination is that the shading algorithm of the environment light is independent of the other positions on the surface except the shading position.  


## 1\. Diffuse Environment Lighting  

Let $\displaystyle \operatorname{L_L}(\overrightarrow{\omega})$ be the distant radiance distribution. Since the Lambert BRDF $\displaystyle \operatorname{f}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V}) = \frac{1}{\pi} \rho_{ss}$ is constant, we have $\displaystyle \operatorname{L_V}(\overrightarrow{\omega_V}) = \int_\Omega \operatorname{f}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V}) \operatorname{L_L}(\overrightarrow{\omega_L}) (\cos \theta_L)^+ \, d \overrightarrow{\omega_L} = \frac{1}{\pi} \rho_{ss} \cdot E$ where $\displaystyle \operatorname{E}(\overrightarrow{n}) = \int_\Omega \operatorname{L_L}(\overrightarrow{\omega_L}) (\cos \theta_L)^+ \, d \overrightarrow{\omega_L} = \int_\Omega \operatorname{L_L}(\overrightarrow{\omega_L}) |\overrightarrow{n} \cdot \overrightarrow{\omega_L}| \, d \overrightarrow{\omega_L}$.  
To keep the circular symmetry of the clamped cosine function, we try to calculate the lighting in tangent space where the normal direction is the Z axis (0, 0, 1). Evidently, we have $\displaystyle \overrightarrow{\omega_L} = R \overrightarrow{\omega_T}$ where R is the rotation transform matrix. And we have $\displaystyle \operatorname{E}(\overrightarrow{n}) = \int_\Omega \operatorname{L_L}(R \overrightarrow{\omega_T}) (\cos \theta_T)^+ \, d \overrightarrow{\omega_T}$.  
Let $\displaystyle \operatorname{\mathcal{SH}}$ be the **SH (Spherical Harmonics) projection operation**. Analogous to the **convolution theorem**, we have $\displaystyle \operatorname{\mathcal{SH}}(\int_\Omega \operatorname{L_L}(R \overrightarrow{\omega_T}) (\cos \theta_T)^+ \, d \overrightarrow{\omega_T}) = \operatorname{\mathcal{SH}}(\operatorname{L_L}(R \overrightarrow{\omega_T})) \operatorname{\mathcal{SH}}((\cos \theta_T)^+)$. Although $\displaystyle \operatorname{\mathcal{SH}}((\cos \theta_T)^+)$ is constant, $\displaystyle \operatorname{\mathcal{SH}}(\operatorname{L_L}(R \overrightarrow{\omega_T}))$ varies by the rotation transform matrix R and is difficult to calculate.  
And let $\displaystyle \operatorname{\mathcal{ZH}}$ be the **ZH (Zonal Harmonics) projection operation**. By \[Ramamoorthi 2001 A\], due to the circular symmetry of $\displaystyle (\cos \theta_T)^+$, we have $\displaystyle \operatorname{\mathcal{SH}}(\int_\Omega \operatorname{L_L}(R \overrightarrow{\omega_T}) (\cos \theta_T)^+ \, d \overrightarrow{\omega_T}) = \sqrt{\frac{4 \pi}{2l + 1}} \operatorname{\mathcal{SH}}(\operatorname{L_L}(\overrightarrow{\omega_L})) \operatorname{\mathcal{ZH}}((\cos \theta_T)^+) = \sqrt{\frac{4 \pi}{2l + 1}} L_L^m A_l$, where $\displaystyle L_L^m = \operatorname{\mathcal{SH}}(\operatorname{L_L}(\overrightarrow{\omega_L}))$ and $\displaystyle A_l = \operatorname{\mathcal{ZH}}((\cos \theta_T)^+)$, which does NOT depend on the rotation transform matrix R.  

### 1-1\. Cubemap Texel Solid Angle

We merely use **numerical quadrature** rather than **Monte Carlo integration** to integrate over the cubemap. But it should be noted that the solid angle subtended by each texel of the cubemap is NOT the same. Let u and v be the texcoord of the cubemap. By "Equation \(5.6\)" of [PBR Book](https://pbr-book.org/3ed-2018/Color_and_Radiometry/Working_with_Radiometric_Integrals#IntegralsoverArea), we have $\displaystyle d\omega = \frac{dA \cos \theta}{r^2} = dA \cdot \cos \theta \cdot \frac{1}{r^2} = \frac{(1 - (-1)) \cdot (1 - (-1))}{\text{cubesize\_u} \cdot \text{cubesize\_v}} \cdot \frac{1}{\sqrt{1^2 + u^2 +v^2}} \cdot \frac{1}{1^2 + u^2 +v^2} = \frac{1}{\text{cubesize\_u} \cdot \text{cubesize\_v}} \cdot \frac{4}{\sqrt{1^2 + u^2 +v^2} \cdot (1^2 + u^2 +v^2)}$. Actually the pseudo code "fWt = 4/(sqrt(fTmp)*fTmp)" by "Projection from Cube Maps" of \[Sloan 2008\] is exactly the $\displaystyle \frac{4}{\sqrt{1^2 + u^2 +v^2} \cdot (1^2 + u^2 +v^2)}$. The common divisor $\displaystyle \frac{1}{\text{cubesize\_u} \cdot \text{cubesize\_v}}$ can be reduced, and thus is NOT calculated by \[Sloan 2008\]. The solid angle is calculated by [SHProjectCubeMap](https://github.com/microsoft/DirectXMath/blob/jul2018b/SHMath/DirectXSHD3D11.cpp#L341) in DirectXMath and [DiffuseIrradianceCopyPS](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/ReflectionEnvironmentShaders.usf#L448) in UE4.  

```MATLAB
% here is the MATLAB code which verifies the meaning of "fWt = 4/(sqrt(fTmp)*fTmp)".

% retrieved by "textureSize(GLSL)" or "GetDimensions(HLSL)".
cube_size_u = 4096.0;
cube_size_v = 4096.0;

[ u, v ] = meshgrid(linspace(-1.0, 1.0, cube_size_u), linspace(-1.0, 1.0, cube_size_v));

% the common divisor "1/(cube_size_u*cube_size_v)" can be reduced, and thus is NOT calculated in the "fWt = 4/(sqrt(fTmp)*fTmp)".
d_a = (1.0 - (-1.0)) .* (1.0 - (-1.0)) ./ cube_size_u ./ cube_size_v;
r_2 = 1.0 .* 1.0 + u .* u + v .* v;
cos_theta = 1.0 ./ sqrt(r_2);
d_omega = d_a .* cos_theta ./ r_2;

% "numerical_omega" and "groundtruth_omega" are expected to be the same.
numerical_omega = sum(sum(d_omega));
groundtruth_omega = 4.0 .* pi .* 1.0 .* 1.0 / 6.0;

% output: "numerical:2.093936 groundtruth:2.094395".
printf("numerical:%f groundtruth:%f\n", numerical_omega, groundtruth_omega);
```  

### 1-2\. Polynomial Forms of SH Basis

By "Appendix A2" of \[Sloan 2008\], we have the **polynomial forms** of SH basis $\displaystyle \operatorname{\Upsilon_l^m}(\overrightarrow{\omega})$. Note that the direction should be normalized before using the polynomial forms. These polynomial forms are calculated by [sh_eval_basis_2](https://github.com/microsoft/DirectXMath/blob/jul2018b/SHMath/DirectXSH.cpp#L132) in DirectXMath, and [SHBasisFunction3](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/SHCommon.ush#L226) in UE4.  

 i  |  l  |  m  | P  
:-: | :-: | :-: | :-  
 0  |  0  |  0  | $\displaystyle \frac{1}{2 \sqrt{\pi}} = 0.282094791773878140$       
 1  |  1  | -1  | $\displaystyle - \frac{\sqrt{3}}{2 \sqrt{\pi}} y = -0.488602511902919920 y$     
 2  |  1  |  0  | $\displaystyle \frac{\sqrt{3}}{2 \sqrt{\pi}} z = 0.488602511902919920 z$     
 3  |  1  |  1  | $\displaystyle - \frac{\sqrt{3}}{2 \sqrt{\pi}} x = -0.488602511902919920 x$     
 4  |  2  | -2  | $\displaystyle \frac{\sqrt{15}}{2 \sqrt{\pi}} x y = 1.092548430592079200 x y$  
 5  |  2  | -1  | $\displaystyle - \frac{\sqrt{15}}{2 \sqrt{\pi}} y z = -1.092548430592079200 y z$    
 6  |  2  |  0  | $\displaystyle \frac{3 \sqrt{5}}{4 \sqrt{\pi}} z^2 - \frac{\sqrt{5}}{4 \sqrt{\pi}} = 0.946174695757560080 z^2 - 0.315391565252520050$     
 7  |  2  |  1  | $\displaystyle - \frac{\sqrt{15}}{2 \sqrt{\pi}} x z = -1.092548430592079200 x z$       
 8  |  2  |  2  | $\displaystyle \frac{\sqrt{15}}{4 \sqrt{\pi}} (x^2 - y^2) = 0.546274215296039590 (x^2 - y^2)$  

### 1-3\. Clamped Cosine  

By \[Ramamoorthi 2001 B\], $\displaystyle \sqrt{\frac{4 \pi}{2l + 1}} A_l$ is constant and can be pre-integrated. For example, by "Figure 5.13" of [PBR Book](https://pbr-book.org/3ed-2018/Color_and_Radiometry/Working_with_Radiometric_Integrals#IntegralsoverProjectedSolidAngle), $\displaystyle A_0$ can pre-integrated as $\displaystyle A_0 = \int_\Omega (\cos \theta)^+ \operatorname{\Upsilon_0^0}(\overrightarrow{\omega}) \, d \overrightarrow{\omega} = \int_\Omega (\cos \theta)^+ \frac{1}{2 \sqrt{\pi}} \, d \overrightarrow{\omega} = \frac{1}{2 \sqrt{\pi}} \int_\Omega (\cos \theta)^+ \, d \overrightarrow{\omega} = \frac{1}{2 \sqrt{\pi}} \, d \overrightarrow{\omega^{\perp}} = \frac{1}{2 \sqrt{\pi}} \pi$. These constants are calculated by [CalcDiffuseTransferSH3](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/SHCommon.ush#L285) in UE4.  

  l | $\displaystyle \sqrt{\frac{4 \pi}{2l + 1}}$ | $\displaystyle A_l$ | $\displaystyle \sqrt{\frac{4 \pi}{2l + 1}} A_l$  
:-: | :-: | :-: | :-:  
  0 | $\displaystyle 2 \sqrt{\pi}$ | $\displaystyle \frac{1}{2 \sqrt{\pi}} \pi$ | $\displaystyle \pi$  
  1 | $\displaystyle \frac{2 \sqrt{\pi}}{\sqrt{3}}$ | $\displaystyle \frac{\sqrt{3}}{2 \sqrt{\pi}} \frac{2\pi}{3}$ | $\displaystyle \frac{2 \pi}{3}$  
  2 | $\displaystyle \frac{2 \sqrt{\pi}}{\sqrt{5}}$ | $\displaystyle \frac{\sqrt{5}}{2 \sqrt{\pi}} \frac{\pi}{4}$ | $\displaystyle \frac{\pi}{4}$  

### 1-4\. Form Factor  

"Appendix A10" of \[Sloan 2008\] proposed a more efficient approach to reconstruct from SH basis than \[Ramamoorthi 2001 B\]. This approach is used by [SampleSH9](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.core/ShaderLibrary/EntityLighting.hlsl#L37) in Unity3D and [GetSkySHDiffuse](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/ReflectionEnvironmentShared.ush#L79) in UE4.  
However, it was **form factor** rather than **irradiance** that "Appendix A10" of \[Sloan 2008\] calculated. Although the terms **irradiance** and **form factor** may be interchangeably used, technically **irradiance** should NOT be divided by $\displaystyle \pi$. This means that $\displaystyle \operatorname{E}(\overrightarrow{n}) = \pi \operatorname{F}(\overrightarrow{n})$. This form factor is calculated by [PackCoefficients](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.high-definition/Runtime/Lighting/SphericalHarmonics.cs#L196) in Unity3D, and [SetupSkyIrradianceEnvironmentMapConstantsFromSkyIrradiance](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Source/Runtime/Renderer/Private/SceneRendering.cpp#L979) and [ComputeSkyEnvMapDiffuseIrradianceCS](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/ReflectionEnvironmentShaders.usf#L607) in UE4.  
And since the value reconstructed from SH basis is form factor rather than irradiance, it should be multiplied by albedo rather than Lambert BRDF. This multiplication is calculated by [GetDiffuseOrDefaultColor](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.high-definition/Runtime/Material/Lit/Lit.hlsl#L1237) in Unity3D and [EnvBRDFApproxFullyRough](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/BasePassPixelShader.usf#L1138) in UE4.  

  fc | value  
 :-: | :-:  
 fC0 | $\displaystyle \frac{1}{\pi} P_0^0 A_0 = \frac{1}{\pi} \frac{1}{2 \sqrt{\pi}} \pi = \frac{1}{2 \sqrt{\pi}}$  
 fc1 | $\displaystyle \frac{1}{\pi} P_1^0 A_1 = \frac{1}{\pi} \frac{\sqrt{3}}{2 \sqrt{\pi}} \frac{2 \pi}{3} = \frac{\sqrt{3}}{3 \sqrt{\pi}}$  
 fc2 | $\displaystyle \frac{1}{\pi} P_2^{-2} A_2 = \frac{1}{\pi} \frac{\sqrt{15}}{2 \sqrt{\pi}} \frac{\pi}{4} = \frac{\sqrt{15}}{8 \sqrt{\pi}}$  
 fc3 | $\displaystyle \frac{1}{\pi} (-P_2^{0}) A_2 = \frac{1}{\pi} \frac{\sqrt{5}}{4 \sqrt{\pi}} \frac{\pi}{4} = \frac{\sqrt{5}}{16 \sqrt{\pi}}$  
 0.3 * fc3 | $\displaystyle \frac{1}{\pi} P_2^{0} A_2 = \frac{1}{\pi} \frac{3 \sqrt{5}}{4 \sqrt{\pi}} \frac{\pi}{4} = \frac{3 \sqrt{5}}{16 \sqrt{\pi}}$  
 fc4 | $\displaystyle \frac{1}{\pi} P_2^{2} A_2 = \frac{1}{\pi} \frac{\sqrt{15}}{4 \sqrt{\pi}} \frac{\pi}{4} = \frac{\sqrt{15}}{16 \sqrt{\pi}}$  

## 2\. Specular Environment Lighting

Let $\displaystyle \operatorname{L}(\overrightarrow{\omega})$ be the distant radiance distribution. Evidently, we have $\displaystyle \operatorname{L_V}(\overrightarrow{\omega_V}) = \int_\Omega \operatorname{f}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V}) \operatorname{L_L}(\overrightarrow{\omega_L}) (\cos \theta_L)^+ \, d \overrightarrow{\omega_L} = \frac{\int_\Omega \operatorname{f}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V}) \operatorname{L_L}(\overrightarrow{\omega_L}) (\cos \theta_L)^+ \, d \overrightarrow{\omega_L}}{\int_\Omega \operatorname{f}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V}) (\cos \theta_L)^+ \, d \overrightarrow{\omega_L}} \cdot \int_\Omega \operatorname{f}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V}) (\cos \theta_L)^+ \, d \overrightarrow{\omega_L} = \operatorname{LD}(\overrightarrow{\omega_V}) \cdot \operatorname{DFG}(\overrightarrow{\omega_V})$ where $\displaystyle \operatorname{LD}(\overrightarrow{\omega_V}) = \frac{\int_\Omega \operatorname{f}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V}) \operatorname{L_L}(\overrightarrow{\omega_L}) (\cos \theta_L)^+ \, d \overrightarrow{\omega_L}}{\int_\Omega \operatorname{f}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V}) (\cos \theta_L)^+ \, d \overrightarrow{\omega_L}}$ and $\operatorname{DFG}(\overrightarrow{\omega_V}) = \int_\Omega \operatorname{f}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V}) (\cos \theta_L)^+ \, d \overrightarrow{\omega_L}$.  

### 2-1\. Monte Carlo Integration  

#### 2-1-1\. PDF  

By "Figure 6" of \[Walter 2007\] and "Figure 14.4" of [PBR Book](https://pbr-book.org/3ed-2018/Light_Transport_I_Surface_Reflection/Sampling_Reflection_Functions#MicrofacetBxDFs), we have the relationship between $\displaystyle d \overrightarrow{\omega_H}$ and $\displaystyle d \overrightarrow{\omega_L}$ that $\displaystyle d \overrightarrow{\omega_H} = \frac{|\overrightarrow{\omega_L} \cdot \overrightarrow{\omega_H}|}{{\|\overrightarrow{\omega_L} + \overrightarrow{\omega_V}\|}^2} d \overrightarrow{\omega_L} = \frac{|\overrightarrow{\omega_L} \cdot \overrightarrow{\omega_H}|}{{\|\overrightarrow{\omega_L} + (2 (\overrightarrow{\omega_L} \cdot \overrightarrow{\omega_H})\overrightarrow{\omega_H} - \overrightarrow{\omega_L})\|}^2} d \overrightarrow{\omega_V} = \frac{|\overrightarrow{\omega_L} \cdot \overrightarrow{\omega_H}|}{4{(\overrightarrow{\omega_L} \cdot \overrightarrow{\omega_H})}^2 {\|\overrightarrow{\omega_H}\|}^2} d \overrightarrow{\omega_L} = \frac{1}{4 |\overrightarrow{\omega_L} \cdot \overrightarrow{\omega_H}|} d \overrightarrow{\omega_L}$. Note that since the subtended area on the sphere surface remains the same, the $\displaystyle d \overrightarrow{\omega_H}$ can be calculated even if the $\displaystyle \overrightarrow{\omega_H}$ is NOT normalized.  

By "Figure 8.15" of [PBR Book](https://pbr-book.org/3ed-2018/Reflection_Models/Microfacet_Models#MicrofacetDistributionFunctions), we have $\displaystyle \int_{\Omega} \operatorname{D}(\overrightarrow{\omega_H}) ( \cos \theta_H )^+ \, d \overrightarrow{\omega_H} = 1$. According to the relationship between $\displaystyle d \overrightarrow{\omega_H}$ and $\displaystyle d \overrightarrow{\omega_L}$, we have $\displaystyle \int_{\Omega} \operatorname{D}(\overrightarrow{\omega_H}) ( \cos \theta_H )^+ \, d \overrightarrow{\omega_H} = \int_{\Omega} \operatorname{D}(\overrightarrow{\omega_H}) ( \cos \theta_H )^+ \frac{1}{4 |\overrightarrow{\omega_L} \cdot \overrightarrow{\omega_H}|} \, d \overrightarrow{\omega_L} = 1$.  Evidently, this normalized function can be used as the PDF $\displaystyle \operatorname{p}(\overrightarrow{\omega_L}) = \operatorname{D}(\overrightarrow{\omega_H}) ( \cos \theta_H )^+ \frac{1}{4 |\overrightarrow{\omega_L} \cdot \overrightarrow{\omega_H}|}$.  

**TODO: Although this is literally the PDF used by UE4, the VNDF by \[Heitz 2018\] is a better alternative to be used as the PDF.**  

By "Equation \(13.3\)" of [PBR Book](https://pbr-book.org/3ed-2018/Monte_Carlo_Integration/The_Monte_Carlo_Estimator), we have $\displaystyle \operatorname{R}(\overrightarrow{\omega_V}) = \int_\Omega \operatorname{f}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V}) (\cos \theta_L)^+ \, d \overrightarrow{\omega_L} = \frac{1}{N} \sum_{i=1}^N \frac{\operatorname{f}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V}) (\cos \theta_L)^+}{\displaystyle \operatorname{p}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V})}$. Evidently, $\displaystyle \operatorname{D}(\overrightarrow{\omega_H})$ exists in both $\displaystyle \operatorname{f}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V})$ and $\displaystyle \operatorname{p}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V})$, and thus $\displaystyle \operatorname{D}(\overrightarrow{\omega_H})$ can be omitted when calculating the integral.  

#### 2-1-2\. Sampling Trowbridge-Reitz Distribution

When $\displaystyle \operatorname{D}(\overrightarrow{\omega_H})$ is **Beckmann–Spizzichino** ("Equation \(8.9\)" of [PBR Book](https://pbr-book.org/3ed-2018/Reflection_Models/Microfacet_Models#MicrofacetDistributionFunctions)) distribution, the derivation of the sampling is provided by "Equation \(14.1\)" of [PBR Book](https://pbr-book.org/3ed-2018/Light_Transport_I_Surface_Reflection/Sampling_Reflection_Functions#MicrofacetBxDFs).  

Analogously, the sampling can be derived when $\displaystyle \operatorname{D}(\overrightarrow{\omega_H})$ is isotropic **Trowbridge-Reitz** ("Equation \(8.11\)" of [PBR Book](https://pbr-book.org/3ed-2018/Reflection_Models/Microfacet_Models#MicrofacetDistributionFunctions)) distribution, namely, **GGX** distribution. Since the distribution is isotropic, we have $\displaystyle \displaystyle \operatorname{p}(\phi | \theta_H) = \frac{1}{2 \pi} \Rightarrow \phi = 2 \pi \xi_2$. Since the PDF is $\displaystyle \operatorname{p}(\overrightarrow{\omega_H}) = \operatorname{D}(\overrightarrow{\omega_H}) ( \cos \theta_H )^+$, we have the marginal PDF $\displaystyle \operatorname{p}(\theta_H) = \int_0^{2 \pi} \operatorname{p}(\theta_H, \phi) \, d \phi =  \int_0^{2 \pi} \operatorname{p}(\overrightarrow{\omega_H}) \sin \omega_H \, d \phi = \int_0^{2 \pi} \operatorname{D}(\overrightarrow{\omega_H}) ( \cos \theta_H )^+ \sin \omega_H \, d \phi = 2 \pi \operatorname{D}(\overrightarrow{\omega_H}) ( \cos \theta_H )^+ \sin \omega_H$ and the CDF $\displaystyle \operatorname{P}(\theta_H) = \int_0^{\theta'_H} \operatorname{p}(\theta'_H) \, d \theta'_H = \xi_1$. Fortunately, this CDF is closed-form and we have $\displaystyle \tan^2 \theta_H = \frac{\alpha^2 \xi_1}{1 - \xi_1} \Rightarrow \cos \theta_H = \frac{1}{\sqrt{1 + \tan^2 \theta_H}} = \sqrt{\frac{1 - \xi_1}{1 + (\alpha^2 - 1) \xi_1}}$.  

Actually, when the PDF is the VNDF by \[Heitz 2018\], the derivation of the sampling is provided by "Equation \(14.2\)" of [PBR Book](https://pbr-book.org/3ed-2018/Light_Transport_I_Surface_Reflection/Sampling_Reflection_Functions#MicrofacetBxDFs).  

The sampling is caculated by [TrowbridgeReitzDistribution::Sample_wh](https://github.com/mmp/pbrt-v3/blob/book/src/core/microfacet.cpp#L308) in PBRT-V3, [ImportanceSampleGGX](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/MonteCarlo.ush#L331) in UE4 and [SampleGGXDir](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.core/ShaderLibrary/ImageBasedLighting.hlsl#L127) in Unity3D.  

#### 2-1-3\. Low-Discrepancy  

By "20.3 Quasirandom Low-Discrepancy Sequences" of \[Colbert 2007\], **Quasi Monte Carlo** ("13.8.2 Quasi Monte Carlo" of [PBR Book](https://pbr-book.org/3ed-2018/Monte_Carlo_Integration/Careful_Sample_Placement#QuasiMonteCarlo)) is used and the pseudo-random sequence is replaced by the low-discrepancy **Hammersley sequence** ("7.4.1 Hammersley and Halton Sequences" of [PBR Book](https://pbr-book.org/3ed-2018/Sampling_and_Reconstruction/The_Halton_Sampler#HammersleyandHaltonSequences)).  

The **Hammersley sequence** is calcuated by [Hammersley](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/MonteCarlo.ush#L34) in UE4 and [Hammersley2d](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.core/ShaderLibrary/Sampling/Hammersley.hlsl#L415) in Unity3D. And the **Fibonacci sequence** is calculated by [FIBONACCI_SEQUENCE_ANGLE](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/SubsurfaceBurleyNormalized.ush#L332) in UE4 and [Fibonacci2d](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.core/ShaderLibrary/Sampling/Fibonacci.hlsl#L248) in Unity3D.  

### 2-2\. DFG Term

Actually, by "Equation \(9.9\)" of [Real-Time Rendering Fourth Edition](https://www.realtimerendering.com/), the DFG term is the HDR (Hemispherical Directional Reflectance) $\displaystyle \operatorname{R}(\overrightarrow{\omega_V}) = \int_\Omega \operatorname{f}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V}) (\cos \theta_L)^+ \, d \omega_L = \int_\Omega \operatorname{f}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V}) (\overrightarrow{(0,0,1)} \cdot \overrightarrow{\omega_L})^+ \, d \omega_L$. Since this integral can be calculated in the tangent space where the normal direction is (0, 0, 1), this integral is independent of the normal direction and can be determined by the view direction in tangent space alone.  

Actually, by "Equation \(9\)" of \[Karis 2013\], the Fresnel term can be treated separately, and we have $\displaystyle \operatorname{R}(\overrightarrow{\omega_V}) = \int_\Omega [F_0 + (F_{90} - F_0) {(1.0 - \overrightarrow{\omega_V} \cdot \overrightarrow{\omega_H})}^5] \operatorname{DV}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V}) \, d \omega_L = F_0 \cdot \operatorname{n_R}(\overrightarrow{\omega_V}) + F_{90} \cdot \operatorname{n_G}(\overrightarrow{\omega_V})$ where $\displaystyle \operatorname{n_R}(\overrightarrow{\omega_V}) = \int_\Omega [1.0 - {(1.0 - \overrightarrow{\omega_V} \cdot \overrightarrow{\omega_H})}^5] \operatorname{DV}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V}) \, d \omega_L$ and $\displaystyle \operatorname{n_G}(\overrightarrow{\omega_V}) = \int_\Omega {(1.0 - \overrightarrow{\omega_V} \cdot \overrightarrow{\omega_H})}^5 \operatorname{DV}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V}) \, d \omega_L$. Evidently, $\displaystyle \operatorname{n_R}(\overrightarrow{\omega_V})$ and $\displaystyle \operatorname{n_G}(\overrightarrow{\omega_V})$ can be stored in the LUT.  

The DFG term is pre-integrated by [InitializeFeatureLevelDependentTextures](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Source/Runtime/Renderer/Private/SystemTextures.cpp#L278) in UE4 and [IntegrateGGXAndDisneyDiffuseFGD](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.core/ShaderLibrary/ImageBasedLighting.hlsl#L340) in Unity3D, and used by [EnvBRDF](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/ReflectionEnvironmentPixelShader.usf#L334) in UE4 and [GetPreIntegratedFGDGGXAndDisneyDiffuse](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.high-definition/Runtime/Material/Lit/Lit.hlsl#L1120) in Unity3D.  

### 2-3\. LD Term

### 2-3-1\. Split Integral Approximation  

By "Equation \(13.3\)" of [PBR Book](https://pbr-book.org/3ed-2018/Monte_Carlo_Integration/The_Monte_Carlo_Estimator), we have $\operatorname{LD}(\overrightarrow{\omega_V}) = \frac{\int_\Omega \operatorname{f}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V}) \operatorname{L_L}(\overrightarrow{\omega_L}) (\cos \theta_L)^+ \, d \overrightarrow{\omega_L}}{\int_\Omega \operatorname{f}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V}) (\cos \theta_L)^+ \, d \overrightarrow{\omega_L}} = \frac{\frac{1}{N} \sum_{i=1}^N \frac{\operatorname{f}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V}) \operatorname{L_L}(\overrightarrow{\omega_L}) (\cos \theta_L)^+}{\displaystyle \operatorname{p}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V})}}{\frac{1}{N} \sum_{i=1}^N \frac{\operatorname{f}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V}) (\cos \theta_L)^+}{\displaystyle \operatorname{p}(\overrightarrow{\omega_L}, \overrightarrow{\omega_V})}} = \frac{\sum_{i=1}^N \frac{\text{D} \cdot \text{F} \cdot \text{G} \cdot \text{L} \cdot (\text{NdotL})^+}{4 \cdot (\text{NdotL})^+ \cdot (\text{NdotV})^+} \frac{4 \cdot (\text{LdotH})^+}{\text{D} \cdot (\text{NdotH})^+}}{\sum_{i=1}^N \frac{\text{D} \cdot \text{F} \cdot \text{G} \cdot (\text{NdotL})^+}{4 \cdot (\text{NdotL})^+ \cdot (\text{NdotV})^+} \frac{4 \cdot (\text{LdotH})^+}{\text{D} \cdot (\text{NdotH})^+}} = \frac{\sum_{i=1}^N \text{L} \frac{\text{F} \cdot \text{G} \cdot (\text{LdotH})^+}{(\text{NdotV})^+ \cdot (\text{NdotH})^+}}{\sum_{i=1}^N \frac{\text{F} \cdot \text{G} \cdot (\text{LdotH})^+}{(\text{NdotV})^+ \cdot (\text{NdotH})^+}} = \frac{\sum_{i=1}^N \text{L} \cdot \text{Weight}}{\sum_{i=1}^N \text{Weight}}$ where $\displaystyle \text{Weight} = \frac{\text{F} \cdot \text{G} \cdot (\text{LdotH})^+}{(\text{NdotV})^+ \cdot (\text{NdotH})^+}$.  

By "Equation \(53\)" of \[Lagarde 2014\], when $\displaystyle \operatorname{L_L}(\overrightarrow{\omega_L})$ is constant, we have $\displaystyle \operatorname{LD}(\overrightarrow{\omega_V}) = \frac{\sum_{i=1}^N \text{L} \cdot \text{Weight}}{\sum_{i=1}^N \text{Weight}} = \frac{\text{L} \cdot \sum_{i=1}^N \text{Weight}}{\sum_{i=1}^N \text{Weight}} = \text{L}$ which does NOT depend on the Weight term. This means that when $\displaystyle \operatorname{L_L}(\overrightarrow{\omega_L})$ is constant, no matter what Weight term we use, we will always have an exact match.    
   
By \[Karis 2013\], assuming that the Weight term equals $\displaystyle (\cos \theta_L)^+$, we have the **split integral approximation** $\displaystyle \operatorname{LD}(\overrightarrow{\omega_V}) = \frac{\sum_{i=1}^N \text{L} \cdot \text{Weight}}{\sum_{i=1}^N \text{Weight}} \approx \frac{\sum_{i=1}^N \text{L} \cdot (\text{NdotL})^+}{\sum_{i=1}^N (\text{NdotL})^+}$.    

The LD term is pre-integrated by [FilterCS](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/ReflectionEnvironmentShaders.usf#L319) in UE4 and [IntegrateLD](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.core/ShaderLibrary/ImageBasedLighting.hlsl#L532) in Unity3D, and used by [GetSkyLightReflection](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/ReflectionEnvironmentShared.ush#L38) in UE4 and [SampleEnvWithDistanceBaseRoughness](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.high-definition/Runtime/Lighting/LightEvaluation.hlsl#L600) in Unity3D.  

#### 2-3-2\. Dimensions   

Ideally, we should use three dimensions: N (world space), NdotV and roughness to look up the pre-integrated LD term.  

By [Karis 2013], roughness is mapped to mip-level.   

The mapping between roughness and mip-level is calculated by [ComputeReflectionCaptureMipFromRoughness](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/ReflectionEnvironmentShared.ush#L21) and [ComputeReflectionCaptureRoughnessFromMip](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/ReflectionEnvironmentShared.ush#L30) in UE4, and [PerceptualRoughnessToMipmapLevel](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.core/ShaderLibrary/ImageBasedLighting.hlsl#L44) and [MipmapLevelToPerceptualRoughness](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.core/ShaderLibrary/ImageBasedLighting.hlsl#L61) by Unity3D.  

However, we do NOT have enough remaining dimensions to store both N (world space) and NdotV. By \[Karis 2013\], we assume "V = N" when pre-integrating the LD term, while the reflection direction R is used to look up the LD term when rendering. By "Figure 10.37" of [Real-Time Rendering Fourth Edition](https://www.realtimerendering.com/), \[Lagarde 2014\] deviates the reflection direction to the normal direction to reduce the error generated by the non-clipped specular lobe.   

The deviation is calculated by [GetOffSpecularPeakReflectionDir](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/ReflectionEnvironmentShared.ush#L120) in UE4 and [GetSpecularDominantDir](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.core/ShaderLibrary/ImageBasedLighting.hlsl#L105) in Unity3D.  

**TODO: If we use the Paraboloid Map, perhaps we can use the 3D texture and provide one dimension for the NdotV. Thus, we can use both N (world space) and NdotV to look up the LD term.**  

#### 2-3-3\. Variance Reduction  

By "20.4 Mipmap Filtered Samples" of \[Colbert 2007\], we use the mip-level $\text{sample\_mip\_level} = \displaystyle \max(0, \log(\sqrt{\frac{d\overrightarrow{\omega_S}}{d\overrightarrow{\omega_P}}}))$ to sample the filtered L value from the distant radiance distribution to reduce the variance. The $\displaystyle d\overrightarrow{\omega_S}$ is the solid angle subtended by the sample, and we have $\displaystyle d\overrightarrow{\omega_S} = \frac{1}{\text{N}} \cdot \frac{1}{\text{PDF}}$. The $\displaystyle d\overrightarrow{\omega_P}$ is the solid angle subtended by a single texel of the zeroth mip-level of the texture, and by "Projection from Cube Maps" of \[Sloan 2008\], we have $\displaystyle d\overrightarrow{\omega_P} = \frac{1}{\text{cubesize\_u} \cdot \text{cubesize\_v}} \cdot \frac{4}{\sqrt{1^2 + u^2 +v^2} \cdot (1^2 + u^2 +v^2)}$.  

The $\displaystyle d\overrightarrow{\omega_S}$ is calculated by [SolidAngleSample](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/ReflectionEnvironmentShaders.usf#L414) in UE4 and [omegaS](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.core/ShaderLibrary/ImageBasedLighting.hlsl#L500) in Unity3D. And the $\displaystyle d\overrightarrow{\omega_P}$ is calculated by [SolidAngleTexel](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/ReflectionEnvironmentShaders.usf#L355) in UE4 and [invOmegaP](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.core/ShaderLibrary/ImageBasedLighting.hlsl#L506) in Unity3D.  

## References  
\[Ramamoorthi 2001 A\] [Ravi Ramamoorthi, Pat Hanrahan. "On the Relationship between Radiance and Irradiance: Determining the illumination from images of a convex Lambertian object." JOSA 2001.](https://graphics.stanford.edu/papers/invlamb/)  
\[Ramamoorthi 2001 B\] [Ravi Ramamoorthi, Pat Hanrahan. "An Efficient Representation for Irradiance Environment Maps." SIGGRAPH 2001.](https://graphics.stanford.edu/papers/envmap/)  
\[Walter 2007\] [Bruce Walter, Stephen Marschner, Hongsong Li, Kenneth Torrance. "Microfacet Models for Refraction through Rough Surfaces." EGSR 2007.](https://www.cs.cornell.edu/~srm/publications/EGSR07-btdf.html)  
\[Colbert 2007\] [Mark Colbert, Jaroslav Krivanek. "GPU-Based Importance Sampling." GPU Gems 3.](https://developer.nvidia.com/gpugems/gpugems3/part-iii-rendering/chapter-20-gpu-based-importance-sampling)  
\[Sloan 2008\] [Peter-Pike Sloan. "Stupid Spherical Harmonics (SH)." Tricks GDC 2008.](http://www.ppsloan.org/publications/StupidSH36.pdf)  
\[Karis 2013\] [Brian Karis. "Real Shading in Unreal Engine 4." SIGGRAPH 2013.](https://cdn2.unrealengine.com/Resources/files/2013SiggraphPresentationsNotes-26915738.pdf)  
\[Lagarde 2014\] [Sebastian Lagarde, Charles Rousiers. "Moving Frostbite to PBR." SIGGRAPH 2014.](https://www.ea.com/frostbite/news/moving-frostbite-to-pb)  
\[Heitz 2018\] [Eric Heitz. "Sampling the GGX Distribution of Visible Normals." JCGT 2018.](https://jcgt.org/published/0007/04/01/)  





