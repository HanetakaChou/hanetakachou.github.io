## Environment Lighting

The name **environment lighting** is from "10.2 Environment Lighting" of [Real-Time Rendering Fourth Edition](https://www.realtimerendering.com/). The most important difference between environment light and global illumination is that the shading algorithm of the environment light is independent of the other positions on the surface except the shading position.  


### Diffuse Environment Lighting  

Let $\displaystyle \operatorname{L_i}(\omega)$ be the infinitely distant radiance distribution. Since the Lambert diffuse BRDF $\displaystyle \operatorname{f}(\overrightarrow{\omega_l}, \overrightarrow{\omega_v}) = \frac{1}{\pi} \rho_{ss}$ is constant, we have $\displaystyle \operatorname{L_o}(\overrightarrow{\omega_v}) = \int_\Omega \operatorname{f}(\overrightarrow{\omega_l}, \overrightarrow{\omega_v}) \operatorname{L_i}(\overrightarrow{\omega_l}) |\cos \theta_l| \, d \overrightarrow{\omega_l} = \frac{1}{\pi} \rho_{ss} \cdot E$ where $\displaystyle E(\overrightarrow{n}) = \int_\Omega \operatorname{L_i}(\overrightarrow{\omega_l}) |\cos \theta_l| \, d \overrightarrow{\omega_l} = \int_\Omega \operatorname{L_i}(\overrightarrow{\omega_l}) |\overrightarrow{n} \cdot \overrightarrow{\omega_l}| \, d \overrightarrow{\omega_l}$. By \[Ramamoorthi 2001\], the irradiance E can be precomputed and stored by SH (Spherical Harmonics).  

### Specular Environment Lighting

Let $\displaystyle \operatorname{L}(\omega)$ denote the infinitely distant radiance distribution.

According to "Equation (9.9)" of [Real-Time Rendering Fourth Edition](https://www.realtimerendering.com/), the DVF term is actually the HDR (hemispherical directional reflectance) $\displaystyle \operatorname{R}(\overrightarrow{\omega_v}) = \int_\Omega \operatorname{f}(\overrightarrow{\omega_l}, \overrightarrow{\omega_v}) |\cos \theta_l| \, d \overrightarrow{\omega_l} = \int_\Omega \operatorname{f}(\overrightarrow{\omega_l}, \overrightarrow{\omega_v}) | \overrightarrow{(0,0,1)} \cdot \overrightarrow{\omega_l}| \, d \overrightarrow{\omega_l}$. Since this integral can be calculated in the tangent space where the normal direction is (0, 0, 1), this integral is independent of the normal direction and can be determined by the view direction in tangent space alone.  
According to the "Equation (9)" of \[Karis 2013\], the Fresnel term can be treated separately, and we have $\displaystyle \operatorname{R}(\overrightarrow{\omega_v}) = \int_\Omega [F_0 + (F_{90} - F_0) {(1.0 - \overrightarrow{\omega_v} \cdot \overrightarrow{\omega_h})}^5] \operatorname{DV}(\overrightarrow{\omega_l}, \overrightarrow{\omega_v}) \, d \overrightarrow{\omega_l} = F_0 \cdot R + F_{90} \cdot G$ where R = $\displaystyle \int_\Omega [1.0 - {(1.0 - \overrightarrow{\omega_v} \cdot \overrightarrow{\omega_h})}^5] \operatorname{DV}(\overrightarrow{\omega_l}, \overrightarrow{\omega_v}) \, d \overrightarrow{\omega_l}$ and G = $\displaystyle \int_\Omega {(1.0 - \overrightarrow{\omega_v} \cdot \overrightarrow{\omega_h})}^5 \operatorname{DV}(\overrightarrow{\omega_l}, \overrightarrow{\omega_v}) \, d \overrightarrow{\omega_l}$. Evidently, R and G can be stored in the LUT and indexed by NdotV and roughness.  
The DVF term is calculated by [EnvBRDF](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/ReflectionEnvironmentPixelShader.usf#L334) in UE4, and [GetPreIntegratedFGDGGXAndDisneyDiffuse](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.high-definition/Runtime/Material/Lit/Lit.hlsl#L1120) in Unity3D.  

## References 
\[Ramamoorthi 2001\] [Ravi Ramamoorthi, Pat Hanrahan. "An Efficient Representation for Irradiance Environment Maps." SIGGRAPH 2001.](https://graphics.stanford.edu/papers/envmap/)  
\[King 2005\] [Gary King. "Real-Time Computation of Dynamic Irradiance Environment Maps." GPU Gems 2.](https://developer.nvidia.com/gpugems/gpugems2/part-ii-shading-lighting-and-shadows/chapter-10-real-time-computation-dynamic)  
\[Colbert 2007\] [Mark Colbert, Jaroslav Krivanek. "GPU-Based Importance Sampling." GPU Gems 3.](https://developer.nvidia.com/gpugems/gpugems3/part-iii-rendering/chapter-20-gpu-based-importance-sampling)  
\[Karis 2013\] [Brian Karis. "Real Shading in Unreal Engine 4." SIGGRAPH 2013.](https://cdn2.unrealengine.com/Resources/files/2013SiggraphPresentationsNotes-26915738.pdf)  
