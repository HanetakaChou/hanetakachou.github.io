# Environment Lighting

The name **environment lighting** is from "10.2 Environment Lighting" of [Real-Time Rendering Fourth Edition](https://www.realtimerendering.com/). By "10.2 Environment Lighting" of [Real-Time Rendering Fourth Edition](https://www.realtimerendering.com/) and "14.4 The Light Transport Equation" of [PBRT-V3](https://pbr-book.org/3ed-2018/Light_Transport_I_Surface_Reflection/The_Light_Transport_Equation), the most important difference between environment lighting (local illumination) and global illumination is that the shading algorithm of the environment lighting (local illumination) is independent of the other positions on the surface except the shading position.  

Notation | Description | Shader Code Convention  
:-: | :-: | :-:  
$\displaystyle \overrightarrow{\omega_o}$ | Outgoing Direction | V  
$\displaystyle \operatorname{L_o}( \overrightarrow{\omega_i})$ | Outgoing Radiance | N/A  
$\displaystyle \overrightarrow{\omega_i}$ | Incident Direction | L  
$\displaystyle \operatorname{f}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o})$ | BRDF | N/A
$\displaystyle \operatorname{L_i}( \overrightarrow{\omega_i})$ | Incident Radiance | N/A
$\displaystyle (\cos \theta_i)^+$ | N/A | clamp(dot(N, L), 0.0, 1.0)  
$\displaystyle \overrightarrow{\omega_h}$ | Half Vector | H  

## 1\. Diffuse Environment Lighting  

Let $\displaystyle \operatorname{L_i}(\overrightarrow{\omega})$ be the distant radiance distribution. Since the Lambert BRDF $\displaystyle \operatorname{f}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o}) = \frac{1}{\pi} \rho_{ss}$ is constant, we have $\displaystyle \operatorname{L_o}(\overrightarrow{\omega_o}) = \int_\Omega \operatorname{f}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o}) \operatorname{L_i}(\overrightarrow{\omega_i}) (\cos \theta_i)^+ \, d \overrightarrow{\omega_i} = \frac{1}{\pi} \rho_{ss} \cdot E$ where $\displaystyle \operatorname{E}(\overrightarrow{n}) = \int_\Omega \operatorname{L_i}(\overrightarrow{\omega_i}) (\cos \theta_i)^+ \, d \overrightarrow{\omega_i} = \int_\Omega \operatorname{L_i}(\overrightarrow{\omega_i}) (\overrightarrow{n} \cdot \overrightarrow{\omega_i})^+ \, d \overrightarrow{\omega_i}$.  

Let $\displaystyle \operatorname{\Upsilon_l^m}(\overrightarrow{\omega})$ be the SH basis function where l is the degree and m is the index from -l to l.  

Let $\displaystyle \operatorname{\mathcal{SH}}$ be the **SH (Spherical Harmonics) projection operation**. Analogous to the **discrete Fourier transform**, we have $\displaystyle k_l^m =\operatorname{\mathcal{SH}}(\operatorname{f}(\overrightarrow{\omega})) = \int_\Omega \operatorname{f}(\overrightarrow{\omega}) \operatorname{\Upsilon_l^m}(\overrightarrow{\omega}) \, d\overrightarrow{\omega}$, and the original function can be reconstructed as the SH series $\displaystyle\operatorname{f}(\overrightarrow{\omega}) = \sum k_l^m \operatorname{\Upsilon_l^m}(\overrightarrow{\omega})$.  

Analogous to the **convolution theorem**, we have $\displaystyle \operatorname{\mathcal{SH}}(\operatorname{E}(\overrightarrow{n})) = \operatorname{\mathcal{SH}}(\int_\Omega \operatorname{L_i}(\overrightarrow{\omega_i}) (\cos \theta_i)^+ \, d \overrightarrow{\omega_i}) = \operatorname{\mathcal{SH}}(\operatorname{L_i}(\overrightarrow{\omega_i})) \operatorname{\mathcal{SH}}((\cos \theta_i)^+)$. Evidently, it is necessary to store the result $\displaystyle \operatorname{\mathcal{SH}}(\operatorname{L_i}(\overrightarrow{\omega_i}))$. But it may be NOT necessary to store the result $\operatorname{\mathcal{SH}}((\cos \theta_i)^+)$, since  the clamped cosine function $\displaystyle (\cos \theta_i)^+$ is constant.  

We try to calculate the lighting in tangent space (where the normal direction is the Z axis $\displaystyle \begin{bmatrix}0 & 0 & 1\end{bmatrix}$) to utilize the circular symmetry of the clamped cosine function $\displaystyle (\cos \theta_i)^+$. Let $\displaystyle \overrightarrow{\omega_i} = \operatorname{R}(\overrightarrow{n}) \overrightarrow{\omega_t}$ where $\displaystyle \operatorname{R}(\overrightarrow{n})$ is the rotation transform matrix and $\displaystyle \overrightarrow{\omega_t}$ is the direction in tangent space. We have $\displaystyle \operatorname{\mathcal{SH}}(\operatorname{E}(\overrightarrow{n})) = \operatorname{\mathcal{SH}}(\int_\Omega \operatorname{L_i}(\operatorname{R}(\overrightarrow{n}) \overrightarrow{\omega_t}) (\cos \theta_t)^+ \, d \overrightarrow{\omega_t}) = \operatorname{\mathcal{SH}}(\operatorname{L_i}(\operatorname{R}(\overrightarrow{n}) \overrightarrow{\omega_t})) \operatorname{\mathcal{SH}}((\cos \theta_t)^+)$. Although $\displaystyle \operatorname{\mathcal{SH}}((\cos \theta_T)^+)$ is constant, $\displaystyle \operatorname{\mathcal{SH}}(\operatorname{L_i}(\operatorname{R}(\overrightarrow{n}) \overrightarrow{\omega_t}))$ depends on the rotation transform matrix $\displaystyle \operatorname{R}(\overrightarrow{n})$ which is a bit difficult to calculate.  

The SH basis function $\displaystyle \operatorname{\Upsilon_l^m}(\overrightarrow{\omega})$ of which the m is zero is called **ZH (zonal harmonics)**.

Let $\displaystyle \operatorname{\mathcal{ZH}}$ be the **ZH (Zonal Harmonics) projection operation**. Analogous to the **discrete Fourier transform**, we have $\displaystyle k_l =\operatorname{\mathcal{ZH}}(\operatorname{f}(\overrightarrow{\omega})) = \int_\Omega \operatorname{f}(\overrightarrow{\omega}) \operatorname{\Upsilon_l^0}(\overrightarrow{\omega}) \, d\overrightarrow{\omega}$, and the original function can be reconstructed as the ZH series $\displaystyle\operatorname{f}(\overrightarrow{\omega}) = \sum k_l \operatorname{\Upsilon_l^0}(\overrightarrow{\omega})$.  

By \[Ramamoorthi 2001 A\], it can be proved that $ E_l^m = \operatorname{\mathcal{SH}}(\operatorname{E}(\overrightarrow{n})) = \operatorname{\mathcal{SH}}(\int_\Omega \operatorname{L_i}(\operatorname{R}(\overrightarrow{n}) \overrightarrow{\omega_t}) (\cos \theta_t)^+ \, d \overrightarrow{\omega_t}) = \sqrt{\frac{4 \pi}{2l + 1}} \operatorname{\mathcal{SH}}(\operatorname{L_i}(\overrightarrow{\omega_i})) \operatorname{\mathcal{ZH}}((\cos \theta_t)^+) = \sqrt{\frac{4 \pi}{2l + 1}} L_l^m A_l$, where $\displaystyle L_l^m = \operatorname{\mathcal{SH}}(\operatorname{L_i}(\overrightarrow{\omega_i}))$ and $\displaystyle A_l = \operatorname{\mathcal{ZH}}((\cos \theta_T)^+)$, which does NOT depend on the rotation transform matrix R.  

### 1-1\. Cubemap Texel Solid Angle

We merely use **numerical quadrature** rather than **Monte Carlo integration** to integrate over the cubemap. But it should be noted that the solid angle subtended by each texel of the cubemap is NOT the same. Let u and v be the texcoord of the cubemap. By "Equation \(5.6\)" of [PBRT-V3](https://pbr-book.org/3ed-2018/Color_and_Radiometry/Working_with_Radiometric_Integrals#IntegralsoverArea), we have $\displaystyle d\omega = \frac{dA \cos \theta}{r^2} = dA \cdot \cos \theta \cdot \frac{1}{r^2} = \frac{(1 - (-1)) \cdot (1 - (-1))}{\text{cubesize\_u} \cdot \text{cubesize\_v}} \cdot \frac{1}{\sqrt{1^2 + u^2 +v^2}} \cdot \frac{1}{1^2 + u^2 +v^2} = \frac{1}{\text{cubesize\_u} \cdot \text{cubesize\_v}} \cdot \frac{4}{\sqrt{1^2 + u^2 +v^2} \cdot (1^2 + u^2 +v^2)}$. Actually the pseudo code "fWt = 4/(sqrt(fTmp)*fTmp)" by "Projection from Cube Maps" of \[Sloan 2008\] is exactly the $\displaystyle \frac{4}{\sqrt{1^2 + u^2 +v^2} \cdot (1^2 + u^2 +v^2)}$. The common divisor $\displaystyle \frac{1}{\text{cubesize\_u} \cdot \text{cubesize\_v}}$ can be reduced, and thus is NOT calculated by \[Sloan 2008\]. The solid angle is calculated by [SHProjectCubeMap](https://github.com/microsoft/DirectXMath/blob/jul2018b/SHMath/DirectXSHD3D11.cpp#L341) in DirectXMath and [DiffuseIrradianceCopyPS](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/ReflectionEnvironmentShaders.usf#L448) in UE4.  

Here is the MATLAB code which verifies the meaning of "fWt = 4/(sqrt(fTmp)*fTmp)".
```MATLAB
% retrieved by "textureSize(GLSL)" or "GetDimensions(HLSL)".
cube_size_u = single(4096.0);
cube_size_v = single(4096.0);

[ index_u, index_v ] = meshgrid((single(0.0) : (cube_size_u - single(1.0))), (single(0.0) : (cube_size_v - single(1.0))));
u = (index_u + single(0.5)) ./ cube_size_u .* single(2.0) - single(1.0);
v = (index_v + single(0.5)) ./ cube_size_u .* single(2.0) - single(1.0);

% the common divisor "1/(cube_size_u*cube_size_v)" can be reduced, and thus is NOT calculated in the "fWt = 4/(sqrt(fTmp)*fTmp)".
d_a = (single(1.0) - single(-1.0)) .* (single(1.0) - single(-1.0)) ./ cube_size_u ./ cube_size_v;
r_2 = single(1.0) .* single(1.0) + single(u) .* single(u) + single(v) .* single(v);
cos_theta = single(1.0) ./ sqrt(r_2);
d_omega = single(d_a) .* single(cos_theta) ./ single(r_2);

% "numerical_omega" and "analytic_omega" are expected to be the same.
numerical_omega = sum(sum(d_omega));
analytical_omega = single(4.0) .* single(pi) .* single(1.0) .* single(1.0) / single(6.0);

% output: "numerical:2.094395 analytic_omega:2.094395".
printf("numerical:%f analytical:%f\n", numerical_omega, analytical_omega);
```  

### 1-2\. Polynomial Forms of SH Basis

By "Appendix A2" of \[Sloan 2008\], we have the **polynomial forms** of SH basis $\displaystyle \operatorname{\Upsilon_l^m}(\overrightarrow{\omega})$. Note that the direction should be **normalized** before using the polynomial forms. These polynomial forms are calculated by [sh_eval_basis_2](https://github.com/microsoft/DirectXMath/blob/jul2018b/SHMath/DirectXSH.cpp#L132) in DirectXMath, and [SHBasisFunction3](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/SHCommon.ush#L226) in UE4.  

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

By \[Ramamoorthi 2001 B\], $\displaystyle \sqrt{\frac{4 \pi}{2l + 1}} A_l$ is constant and can be pre-integrated. For example, by "Figure 5.13" of [PBRT-V3](https://pbr-book.org/3ed-2018/Color_and_Radiometry/Working_with_Radiometric_Integrals#IntegralsoverProjectedSolidAngle), $\displaystyle A_0$ can pre-integrated as $\displaystyle A_0 = \int_\Omega (\cos \theta)^+ \operatorname{\Upsilon_0^0}(\overrightarrow{\omega}) \, d \overrightarrow{\omega} = \int_\Omega (\cos \theta)^+ \frac{1}{2 \sqrt{\pi}} \, d \overrightarrow{\omega} = \frac{1}{2 \sqrt{\pi}} \int_\Omega (\cos \theta)^+ \, d \overrightarrow{\omega} = \frac{1}{2 \sqrt{\pi}} \, d \overrightarrow{\omega^{\perp}} = \frac{1}{2 \sqrt{\pi}} \pi$. These constants are calculated by [CalcDiffuseTransferSH3](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/SHCommon.ush#L285) in UE4.  

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
 fc0 | $\displaystyle \frac{1}{\pi} P_0^0 A_0 = \frac{1}{\pi} \frac{1}{2 \sqrt{\pi}} \pi = \frac{1}{2 \sqrt{\pi}}$  
 fc1 | $\displaystyle \frac{1}{\pi} P_1^0 A_1 = \frac{1}{\pi} \frac{\sqrt{3}}{2 \sqrt{\pi}} \frac{2 \pi}{3} = \frac{\sqrt{3}}{3 \sqrt{\pi}}$  
 fc2 | $\displaystyle \frac{1}{\pi} P_2^{-2} A_2 = \frac{1}{\pi} \frac{\sqrt{15}}{2 \sqrt{\pi}} \frac{\pi}{4} = \frac{\sqrt{15}}{8 \sqrt{\pi}}$  
 fc3 | $\displaystyle \frac{1}{\pi} (-P_2^{0}) A_2 = \frac{1}{\pi} \frac{\sqrt{5}}{4 \sqrt{\pi}} \frac{\pi}{4} = \frac{\sqrt{5}}{16 \sqrt{\pi}}$  
 0.3 * fc3 | $\displaystyle \frac{1}{\pi} P_2^{0} A_2 = \frac{1}{\pi} \frac{3 \sqrt{5}}{4 \sqrt{\pi}} \frac{\pi}{4} = \frac{3 \sqrt{5}}{16 \sqrt{\pi}}$  
 fc4 | $\displaystyle \frac{1}{\pi} P_2^{2} A_2 = \frac{1}{\pi} \frac{\sqrt{15}}{4 \sqrt{\pi}} \frac{\pi}{4} = \frac{\sqrt{15}}{16 \sqrt{\pi}}$  

## 2\. Specular Environment Lighting

Let $\displaystyle \operatorname{L}(\overrightarrow{\omega})$ be the distant radiance distribution. Evidently, we have $\displaystyle \operatorname{L_o}(\overrightarrow{\omega_o}) = \int_\Omega \operatorname{f}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o}) \operatorname{L_i}(\overrightarrow{\omega_i}) (\cos \theta_i)^+ \, d \overrightarrow{\omega_i} = \frac{\int_\Omega \operatorname{f}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o}) \operatorname{L_i}(\overrightarrow{\omega_i}) (\cos \theta_i)^+ \, d \overrightarrow{\omega_i}}{\int_\Omega \operatorname{f}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o}) (\cos \theta_i)^+ \, d \overrightarrow{\omega_i}} \cdot \int_\Omega \operatorname{f}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o}) (\cos \theta_i)^+ \, d \overrightarrow{\omega_i} = \operatorname{LD}(\overrightarrow{\omega_o}) \cdot \operatorname{DFG}(\overrightarrow{\omega_o})$ where $\displaystyle \operatorname{LD}(\overrightarrow{\omega_o}) = \frac{\int_\Omega \operatorname{f}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o}) \operatorname{L_i}(\overrightarrow{\omega_i}) (\cos \theta_i)^+ \, d \overrightarrow{\omega_i}}{\int_\Omega \operatorname{f}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o}) (\cos \theta_i)^+ \, d \overrightarrow{\omega_i}}$ and $\operatorname{DFG}(\overrightarrow{\omega_o}) = \int_\Omega \operatorname{f}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o}) (\cos \theta_i)^+ \, d \overrightarrow{\omega_i}$.  

### 2-1\. Monte Carlo Integration  

#### 2-1-1\. PDF - NDF 

Let $\displaystyle \overrightarrow{\omega_h} = \frac{\overrightarrow{\omega_i} + \overrightarrow{\omega_o}}{\| \overrightarrow{\omega_i} + \overrightarrow{\omega_o} \|}$ be the half vector. By "Equation (5.6)" of [PBRT-V3](https://pbr-book.org/3ed-2018/Color_and_Radiometry/Working_with_Radiometric_Integrals#IntegralsoverArea), "Figure 6" of \[Walter 2007\] and "Figure 14.4" of [PBRT-V3](https://pbr-book.org/3ed-2018/Light_Transport_I_Surface_Reflection/Sampling_Reflection_Functions#MicrofacetBxDFs), we have the relationship between $\displaystyle d \overrightarrow{\omega_h}$ and $\displaystyle d \overrightarrow{\omega_i}$ that $\displaystyle d \overrightarrow{\omega_h} =  \frac{\cos\theta}{r^2} d A = \frac{|\overrightarrow{\omega_i} \cdot \overrightarrow{\omega_h}|}{{\|\overrightarrow{\omega_i} + \overrightarrow{\omega_o}\|}^2} d \overrightarrow{\omega_i} = \frac{|\overrightarrow{\omega_i} \cdot \overrightarrow{\omega_h}|}{{\|\overrightarrow{\omega_i} + (2 (\overrightarrow{\omega_i} \cdot \overrightarrow{\omega_h})\overrightarrow{\omega_h} - \overrightarrow{\omega_i})\|}^2} d \overrightarrow{\omega_o} = \frac{|\overrightarrow{\omega_i} \cdot \overrightarrow{\omega_h}|}{4{(\overrightarrow{\omega_i} \cdot \overrightarrow{\omega_h})}^2 {\|\overrightarrow{\omega_h}\|}^2} d \overrightarrow{\omega_i} = \frac{1}{4 |\overrightarrow{\omega_i} \cdot \overrightarrow{\omega_h}|} d \overrightarrow{\omega_i}$. Note that since the subtended area on the sphere surface remains the same, the $\displaystyle d \overrightarrow{\omega_h}$ can be calculated even if the $\displaystyle \overrightarrow{\omega_h}$ is NOT normalized.  

By "Equation \(9\)" of \[Heitz 2014\] and "Figure 8.15" of [PBRT-V3](https://pbr-book.org/3ed-2018/Reflection_Models/Microfacet_Models#MicrofacetDistributionFunctions), we have $\displaystyle \int_{\Omega} \operatorname{D}(\overrightarrow{\omega_h}) ( \cos \theta_h )^+ \, d \overrightarrow{\omega_h} = 1$. According to the relationship between $\displaystyle d \overrightarrow{\omega_h}$ and $\displaystyle d \overrightarrow{\omega_i}$, we have $\displaystyle \int_{\Omega} \operatorname{D}(\overrightarrow{\omega_h}) ( \cos \theta_h )^+ \, d \overrightarrow{\omega_h} = \int_{\Omega} \operatorname{D}(\overrightarrow{\omega_h}) ( \cos \theta_h )^+ \frac{1}{4 |\overrightarrow{\omega_i} \cdot \overrightarrow{\omega_h}|} \, d \overrightarrow{\omega_i} = 1$.  Evidently, this normalized function can be used as the PDF $\displaystyle \operatorname{p}(\overrightarrow{\omega_i}) = \operatorname{D}(\overrightarrow{\omega_h}) ( \cos \theta_h )^+ \frac{1}{4 |\overrightarrow{\omega_i} \cdot \overrightarrow{\omega_h}|}$.  

#### 2-1-2\. PDF - VNDF  

Genuinely, although the NDF is the PDF used by UE4, the VNDF by \[Heitz 2018\] is the better alternative.  

By "Equation (14)" of \[Heitz 2014\] and "Equation \(8.12\)" of [PBRT-V3](https://pbr-book.org/3ed-2018/Reflection_Models/Microfacet_Models#MaskingandShadowing), we have $\displaystyle \int_{\Omega} \operatorname{G_1}(\overrightarrow{\omega_o},  \overrightarrow{\omega_h}) ( \overrightarrow{\omega_o} \cdot  \overrightarrow{\omega_h} )^+ \operatorname{D}(\overrightarrow{\omega_h}) \, d \overrightarrow{\omega_h} = \cos \theta_o$.  

**TODO:**  

#### 2-1-3\. Sampling Trowbridge-Reitz Distribution - NDF

For **Beckmann–Spizzichino** ("Equation \(8.9\)" of [PBRT-V3](https://pbr-book.org/3ed-2018/Reflection_Models/Microfacet_Models#MicrofacetDistributionFunctions)) distribution, the derivation of the NDF sampling is provided by "Equation \(14.1\)" of [PBRT-V3](https://pbr-book.org/3ed-2018/Light_Transport_I_Surface_Reflection/Sampling_Reflection_Functions#MicrofacetBxDFs).  

For isotropic **Trowbridge-Reitz** ("Equation \(8.11\)" of [PBRT-V3](https://pbr-book.org/3ed-2018/Reflection_Models/Microfacet_Models#MicrofacetDistributionFunctions)) distribution, namely, **GGX** distribution, the NDF sampling can be analogously derived. Since the distribution is isotropic, we have $\displaystyle \displaystyle \operatorname{p}(\phi | \theta_h) = \frac{1}{2 \pi} \Rightarrow \phi = 2 \pi \xi_2$. Since the PDF is $\displaystyle \operatorname{p}(\overrightarrow{\omega_h}) = \operatorname{D}(\overrightarrow{\omega_h}) ( \cos \theta_h )^+$,  by "13.5.3 Spherical Coordinates" of [PBRT-V3](https://pbr-book.org/3ed-2018/Monte_Carlo_Integration/Transforming_between_Distributions#SphericalCoordinates), we have the marginal PDF $\displaystyle \operatorname{p}(\theta_h) = \int_0^{2 \pi} \operatorname{p}(\theta_h, \phi) \, d \phi =  \int_0^{2 \pi} \operatorname{p}(\overrightarrow{\omega_h}) \sin \theta_h \, d \phi = \int_0^{2 \pi} \operatorname{D}(\overrightarrow{\omega_h}) ( \cos \theta_h )^+ \sin \theta_h \, d \phi = 2 \pi \operatorname{D}(\overrightarrow{\omega_h}) ( \cos \theta_h )^+ \sin \theta_h$ and the CDF $\displaystyle \operatorname{P}(\theta_h) = \int_0^{\theta_h} \operatorname{p}(\theta'_h) \, d \theta'_h = \xi_1$. Fortunately, the inverse of the CDF is closed-form and we have $\displaystyle \tan^2 \theta_h = \frac{\alpha^2 \xi_1}{1 - \xi_1} \Rightarrow \cos \theta_h = \frac{1}{\sqrt{1 + \tan^2 \theta_h}} = \sqrt{\frac{1 - \xi_1}{1 + (\alpha^2 - 1) \xi_1}}$.  

The NDF sampling is calculated by [TrowbridgeReitzDistribution::Sample_wh](https://github.com/mmp/pbrt-v3/blob/book/src/core/microfacet.cpp#L308) in PBRT-V3, [ImportanceSampleGGX](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/MonteCarlo.ush#L331) in UE4 and [SampleGGXDir](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.core/ShaderLibrary/ImageBasedLighting.hlsl#L127) in Unity3D.  


#### 2-1-4\. Sampling Trowbridge-Reitz Distribution - VNDF

For **Beckmann–Spizzichino** ("Equation \(8.9\)" of [PBRT-V3](https://pbr-book.org/3ed-2018/Reflection_Models/Microfacet_Models#MicrofacetDistributionFunctions)) distribution, the derivation of the VNDF sampling is provided by "Equation \(14.2\)" of [PBRT-V3](https://pbr-book.org/3ed-2018/Light_Transport_I_Surface_Reflection/Sampling_Reflection_Functions#MicrofacetBxDFs).  

**TODO:**  

#### 2-1-5\. Low-Discrepancy Sequence  
  
By "20.3 Quasirandom Low-Discrepancy Sequences" of \[Colbert 2007\] and "13.8.2 Quasi Monte Carlo" of [PBRT-V3](https://pbr-book.org/3ed-2018/Monte_Carlo_Integration/Careful_Sample_Placement#QuasiMonteCarlo), the **low-discrepancy sequence** is the better alternative than **pseudo-random sequence** to generate the $\displaystyle \xi_1$ and $\displaystyle \xi_2$.  

For example, the **Hammersley sequence** ("7.4.1 Hammersley and Halton Sequences" of [PBRT-V3](https://pbr-book.org/3ed-2018/Sampling_and_Reconstruction/The_Halton_Sampler#HammersleyandHaltonSequences)) is a typical **low-discrepancy sequence**.  

The **Hammersley sequence** is calculated by [Hammersley](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/MonteCarlo.ush#L34) in UE4 and [Hammersley2d](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.core/ShaderLibrary/Sampling/Hammersley.hlsl#L415) in Unity3D.  
   
### 2-2\. DFG Term

By "Equation \(9.9\)" of [Real-Time Rendering Fourth Edition](https://www.realtimerendering.com/), the DFG term is the HDR (Hemispherical Directional Reflectance) $\displaystyle \operatorname{R}(\overrightarrow{\omega_o}) = \int_\Omega \operatorname{f}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o}) (\cos \theta_i)^+ \, d \overrightarrow{\omega_i} = \int_\Omega \operatorname{f}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o}) (\overrightarrow{(0,0,1)} \cdot \overrightarrow{\omega_i})^+ \, d \overrightarrow{\omega_i}$. Since this integral can be calculated in the tangent space where the normal direction is (0, 0, 1), this integral is independent of the normal direction and can be determined by the view direction in tangent space alone.  

And by "Equation \(13.3\)" of [PBRT-V3](https://pbr-book.org/3ed-2018/Monte_Carlo_Integration/The_Monte_Carlo_Estimator), we have $\displaystyle \operatorname{R}(\overrightarrow{\omega_o}) = \int_\Omega \operatorname{f}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o}) (\cos \theta_i)^+ \, d \overrightarrow{\omega_i} = \frac{1}{N} \sum_{i=1}^N \frac{\operatorname{f}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o}) (\cos \theta_i)^+}{\displaystyle \operatorname{p}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o})}$. Evidently, $\displaystyle \operatorname{D}(\overrightarrow{\omega_h})$ exists in both $\displaystyle \operatorname{f}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o})$ and $\displaystyle \operatorname{p}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o})$, and thus $\displaystyle \operatorname{D}(\overrightarrow{\omega_h})$ can be omitted when calculating the integral.  

Actually, by "Equation \(9\)" of \[Karis 2013\], the Fresnel term can be treated separately, and we have $\displaystyle \operatorname{R}(\overrightarrow{\omega_o}) = \int_\Omega [F_0 + (F_{90} - F_0) {(1.0 - \overrightarrow{\omega_o} \cdot \overrightarrow{\omega_h})}^5] \operatorname{DV}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o}) \, d \overrightarrow{\omega_i} = F_0 \cdot \operatorname{n_R}(\overrightarrow{\omega_o}) + F_{90} \cdot \operatorname{n_G}(\overrightarrow{\omega_o})$ where $\displaystyle \operatorname{n_R}(\overrightarrow{\omega_o}) = \int_\Omega [1.0 - {(1.0 - \overrightarrow{\omega_o} \cdot \overrightarrow{\omega_h})}^5] \operatorname{DV}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o}) \, d \overrightarrow{\omega_i}$ and $\displaystyle \operatorname{n_G}(\overrightarrow{\omega_o}) = \int_\Omega {(1.0 - \overrightarrow{\omega_o} \cdot \overrightarrow{\omega_h})}^5 \operatorname{DV}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o}) \, d \overrightarrow{\omega_i}$. Evidently, $\displaystyle \operatorname{n_R}(\overrightarrow{\omega_o})$ and $\displaystyle \operatorname{n_G}(\overrightarrow{\omega_o})$ can be stored in the LUT.  

The DFG term is pre-integrated by [InitializeFeatureLevelDependentTextures](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Source/Runtime/Renderer/Private/SystemTextures.cpp#L278) in UE4 and [IntegrateGGXAndDisneyDiffuseFGD](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.core/ShaderLibrary/ImageBasedLighting.hlsl#L340) in Unity3D, and used by [EnvBRDF](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/ReflectionEnvironmentPixelShader.usf#L334) in UE4 and [GetPreIntegratedFGDGGXAndDisneyDiffuse](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.high-definition/Runtime/Material/Lit/Lit.hlsl#L1120) in Unity3D.  

### 2-3\. LD Term

#### 2-3-1\. Split Integral Approximation  

By "Equation \(13.3\)" of [PBRT-V3](https://pbr-book.org/3ed-2018/Monte_Carlo_Integration/The_Monte_Carlo_Estimator), we have $\operatorname{LD}(\overrightarrow{\omega_o}) = \frac{\int_\Omega \operatorname{f}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o}) \operatorname{L_i}(\overrightarrow{\omega_i}) (\cos \theta_i)^+ \, d \overrightarrow{\omega_i}}{\int_\Omega \operatorname{f}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o}) (\cos \theta_i)^+ \, d \overrightarrow{\omega_i}} = \frac{\frac{1}{N} \sum_{i=1}^N \frac{\operatorname{f}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o}) \operatorname{L_i}(\overrightarrow{\omega_i}) (\cos \theta_i)^+}{\displaystyle \operatorname{p}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o})}}{\frac{1}{N} \sum_{i=1}^N \frac{\operatorname{f}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o}) (\cos \theta_i)^+}{\displaystyle \operatorname{p}(\overrightarrow{\omega_i}, \overrightarrow{\omega_o})}} = \frac{\sum_{i=1}^N \frac{\text{D} \cdot \text{F} \cdot \text{G} \cdot \text{L} \cdot (\text{NdotL})^+}{4 \cdot (\text{NdotL})^+ \cdot (\text{NdotV})^+} \frac{4 \cdot (\text{LdotH})^+}{\text{D} \cdot (\text{NdotH})^+}}{\sum_{i=1}^N \frac{\text{D} \cdot \text{F} \cdot \text{G} \cdot (\text{NdotL})^+}{4 \cdot (\text{NdotL})^+ \cdot (\text{NdotV})^+} \frac{4 \cdot (\text{LdotH})^+}{\text{D} \cdot (\text{NdotH})^+}} = \frac{\sum_{i=1}^N \text{L} \frac{\text{F} \cdot \text{G} \cdot (\text{LdotH})^+}{(\text{NdotV})^+ \cdot (\text{NdotH})^+}}{\sum_{i=1}^N \frac{\text{F} \cdot \text{G} \cdot (\text{LdotH})^+}{(\text{NdotV})^+ \cdot (\text{NdotH})^+}} = \frac{\sum_{i=1}^N \text{L} \cdot \text{Weight}}{\sum_{i=1}^N \text{Weight}}$ where $\displaystyle \text{Weight} = \frac{\text{F} \cdot \text{G} \cdot (\text{LdotH})^+}{(\text{NdotV})^+ \cdot (\text{NdotH})^+}$.  

By "Equation \(53\)" of \[Lagarde 2014\], when $\displaystyle \operatorname{L_i}(\overrightarrow{\omega_i})$ is constant, we have $\displaystyle \operatorname{LD}(\overrightarrow{\omega_o}) = \frac{\sum_{i=1}^N \text{L} \cdot \text{Weight}}{\sum_{i=1}^N \text{Weight}} = \frac{\text{L} \cdot \sum_{i=1}^N \text{Weight}}{\sum_{i=1}^N \text{Weight}} = \text{L}$ which does NOT depend on the Weight term. This means that when $\displaystyle \operatorname{L_i}(\overrightarrow{\omega_i})$ is constant, no matter what Weight term we use, we will always have an exact match.    
   
By \[Karis 2013\], assuming that the Weight term equals $\displaystyle (\cos \theta_i)^+$, we have the **split integral approximation** $\displaystyle \operatorname{LD}(\overrightarrow{\omega_o}) = \frac{\sum_{i=1}^N \text{L} \cdot \text{Weight}}{\sum_{i=1}^N \text{Weight}} \approx \frac{\sum_{i=1}^N \text{L} \cdot (\text{NdotL})^+}{\sum_{i=1}^N (\text{NdotL})^+}$.    

The LD term is pre-integrated by [FilterCS](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/ReflectionEnvironmentShaders.usf#L319) in UE4 and [IntegrateLD](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.core/ShaderLibrary/ImageBasedLighting.hlsl#L532) in Unity3D, and used by [GetSkyLightReflection](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/ReflectionEnvironmentShared.ush#L38) in UE4 and [SampleEnvWithDistanceBaseRoughness](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.high-definition/Runtime/Lighting/LightEvaluation.hlsl#L600) in Unity3D.  

#### 2-3-2\. Dimensions   

Ideally, we should use three dimensions: N (world space), NdotV and roughness to look up the pre-integrated LD term.  

By [Karis 2013], roughness is mapped to mip-level.   

The mapping between roughness and mip-level is calculated by [ComputeReflectionCaptureMipFromRoughness](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/ReflectionEnvironmentShared.ush#L21) and [ComputeReflectionCaptureRoughnessFromMip](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/ReflectionEnvironmentShared.ush#L30) in UE4, and [PerceptualRoughnessToMipmapLevel](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.core/ShaderLibrary/ImageBasedLighting.hlsl#L44) and [MipmapLevelToPerceptualRoughness](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.core/ShaderLibrary/ImageBasedLighting.hlsl#L61) in Unity3D.  

However, we do NOT have enough remaining dimensions to store both N (world space) and NdotV. By \[Karis 2013\], we assume "V = N" when pre-integrating the LD term, while the reflection direction R is used to look up the LD term when rendering. By "Figure 10.37" of [Real-Time Rendering Fourth Edition](https://www.realtimerendering.com/), by \[Lagarde 2014\], the reflection direction is biased towards the normal direction to reduce the error generated by the non-clipped specular lobe.   

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
\[Heitz 2014\] [Eric Heitz. "Understanding the Masking-Shadowing Function in Microfacet-Based BRDFs." JCGT 2014.](https://jcgt.org/published/0003/02/03/)  
\[Heitz 2018\] [Eric Heitz. "Sampling the GGX Distribution of Visible Normals." JCGT 2018.](https://jcgt.org/published/0007/04/01/)  







