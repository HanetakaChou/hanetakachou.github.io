# VCT (Voxel Cone Tracing)  

Notation | Description | Shader Code Convention  
:-: | :-: | :-:  
$\displaystyle \overrightarrow{p}$ | Surface Position in World Space | N/A  
$\displaystyle \overrightarrow{\omega_i}$ | Incident Direction in Tangent Space | L  
$\displaystyle \overrightarrow{\omega_o}$ | Outgoing Direction in Tangent Space | V  
$\displaystyle \overrightarrow{\omega_h}$ | Half Vector in Tangent Space | H  
$\displaystyle \overrightarrow{n}$ | Normal in World Space | N  
$\displaystyle \operatorname{f}(\overrightarrow{p}, \overrightarrow{\omega_i}, \overrightarrow{\omega_o})$ | BRDF | N/A  
$\displaystyle \operatorname{L_i}(\overrightarrow{p}, \overrightarrow{\omega_i})$ | Incident Radiance | N/A
$\displaystyle \operatorname{L_o}(\overrightarrow{p}, \overrightarrow{\omega_o})$ | Outgoing Radiance | N/A  
$\displaystyle \max(0, \cos \theta_i)$ | Clamped Cosine | NdotL  


## 1\. Theoretical Background  

### 1-1\. Photon Mapping  

By "4.3 Overview" of \[Jensen 2001\] and \[Hachisuka 2005\], the **photon mapping** is composed of two steps: **photon tracing** and **rendering**. During the **photon tracing** step, the **photon rays** are traced from the light sources, and the lighting information of the intersection positions of these **photon rays** is recorded as the photons. During the **rendering** step, the **primary rays** are traced from the camera and the **final gather rays** are traced from the [**final gather points**](http://docs.autodesk.com/MENTALRAY/2015/ENU/mental-ray-help/files/manual/node52.html), and the lighting information of the neighboring photons of the intersection positions of these **primary rays** or **final gather rays** is used to approximate the lighting of these intersection points.  

By \[Crassin 2011\], the **VCT (Voxel Cone Tracing)** is composed of three steps: **light injection**, **filtering** and **cone tracing**. The idea of the voxel cone tracing is intrinsically to implement the photon mapping by storing the photons in the voxels. The **voxelization** (**light injection** and **filtering**) step of the voxel cone tracing is analogous to the **photon tracing** step of the photon mapping. The **cone tracing** step of the voxel cone tracing is analogous to the **rendering** step of the photon mapping.  

Given N photons at position $\displaystyle \overrightarrow{p_j}$ within the neighborhood of position $\displaystyle \overrightarrow{p_0}$, we have the approximation of the outgoing radiance at position $\displaystyle \overrightarrow{p_0}$ that $\displaystyle \operatorname{L_o}(\overrightarrow{p_0}, \overrightarrow{\omega_o}) \approx \frac{1}{\mathrm{NeighborhoodArea}} \sum_{j=0}^N \operatorname{f}(\overrightarrow{p_j}, \overrightarrow{\omega_i}, \overrightarrow{\omega_o}) \operatorname{\Delta\Phi}(\overrightarrow{p_j})$.  

> Proof  
>  
> We assume that $\displaystyle \operatorname{L_i}(\overrightarrow{p}, \overrightarrow{\omega_i})$ is the indicent radiance distribution on position direction space $\displaystyle \operatorname{B_r}(\overrightarrow{p_0}) \times {\mathrm{S}}^2$ (of which $\displaystyle \operatorname{B_r}(\overrightarrow{p_0})$ is the neighborhood with center $\displaystyle \overrightarrow{p_0}$ and radius r, and $\displaystyle {\mathrm{S}}^2$ is the sphere).  
>  
> Evidently, we have the total flux over the whole neighborhood $\displaystyle \mathrm{\Phi} = \int_{\operatorname{B_r}(\overrightarrow{p_0})} \int_{{\mathrm{S}}^2} \operatorname{L_i}(\overrightarrow{p}, \overrightarrow{\omega_i}) \max(0, \cos \theta_i) \, d \omega \, d \operatorname{A}(\overrightarrow{p})$. And we have the normalized PDF $\displaystyle \operatorname{p}(\overrightarrow{p}, \overrightarrow{\omega_i}) = \frac{\operatorname{L_i}(\overrightarrow{p}, \overrightarrow{\omega_i}) \max(0, \cos \theta_i)}{\mathrm{\Phi}}$.  
>  
> We assume that within the neighborhood are N samples (namely, photons) $\displaystyle \operatorname{\Delta\Phi}(\overrightarrow{p_j})$ such that the expectation $\displaystyle \operatorname{\mathbb{E}_p}\left(\sum_{j=1}^N \operatorname{\Delta\Phi}(\overrightarrow{p_j}) \right) = \int_{\operatorname{B_r}(\overrightarrow{p_0})} \int_{{\mathrm{S}}^2} \operatorname{L_i}(\overrightarrow{p}, \overrightarrow{\omega_i}) \max(0, \cos \theta_i) \, d \omega \, d \operatorname{A}(\overrightarrow{p}) = \mathrm{\Phi}$.  
>  
> By "Equation 16.7" of [PBR Book V3](https://www.pbr-book.org/3ed-2018/Light_Transport_III_Bidirectional_Methods/Stochastic_Progressive_Photon_Mapping#TheoreticalBasisforParticleTracing), given the uniform kernel $\displaystyle \operatorname{K}(\overrightarrow{p_0}, \overrightarrow{p}) = \frac{1}{\operatorname{Area}(\operatorname{B_r}(\overrightarrow{p_0}))}$, we have the expectation $\displaystyle \operatorname{\mathbb{E}_p}\left(\sum_{j=1}^N \operatorname{K}(\overrightarrow{p_0}, \overrightarrow{p_j}) \operatorname{f}(\overrightarrow{p_j}, \overrightarrow{\omega_i}, \overrightarrow{\omega_o}) \operatorname{\Delta\Phi}(\overrightarrow{p_j}) \right) = \int_{\operatorname{B_r}(\overrightarrow{p_0})} \int_{{\mathrm{S}}^2} \operatorname{K}(\overrightarrow{p_0}, \overrightarrow{p}) \operatorname{f}(\overrightarrow{p}, \overrightarrow{\omega_i}, \overrightarrow{\omega_o}) \operatorname{L_i}(\overrightarrow{p}, \overrightarrow{\omega_i}) \max(0, \cos \theta_i) \, d \omega \, d \operatorname{A}(\overrightarrow{p})$.  
>  
> By "Equation 16.9" of [PBR Book V3](https://pbr-book.org/3ed-2018/Light_Transport_III_Bidirectional_Methods/Stochastic_Progressive_Photon_Mapping#PhotonMapping), since $\displaystyle \operatorname{K}(\overrightarrow{p_0}, \overrightarrow{p})$ is the dirac delta distribution when r tends to zero, we have that $\displaystyle \lim\limits_{r \rightarrow 0} \operatorname{\mathbb{E}_p}\left(\sum_{j=1}^N \operatorname{K}(\overrightarrow{p_0}, \overrightarrow{p_j}) \operatorname{f}(\overrightarrow{p_j}, \overrightarrow{\omega_i}, \overrightarrow{\omega_o}) \operatorname{\Delta\Phi}(\overrightarrow{p_j}) \right) = \int_{{\mathrm{S}}^2} \operatorname{f}(\overrightarrow{p_0}, \overrightarrow{\omega_i}, \overrightarrow{\omega_o}) \operatorname{L_i}(\overrightarrow{p_0}, \overrightarrow{\omega_i}) \max(0, \cos \theta_i) \, d \omega = \operatorname{L_o}(\overrightarrow{p_0}, \overrightarrow{\omega_o})$ which is exactly the "Equation 7.6" of \[Jensen 2001\].  

By "Equation 16.15" of [PBR Book V3](https://pbr-book.org/3ed-2018/Light_Transport_III_Bidirectional_Methods/Stochastic_Progressive_Photon_Mapping#AccumulatingPhotonContributions), in real time rendering, we have the approximation of the $\displaystyle \operatorname{\Delta\Phi}(\overrightarrow{p_j})$ at position $\displaystyle \overrightarrow{p_j}$ that $\displaystyle \operatorname{\Delta\Phi}(\overrightarrow{p_j}) \approx \operatorname{E_N}(\overrightarrow{p_j}) \cdot \mathrm{PhotonArea} = \operatorname{E_L}(\overrightarrow{p_j}) \cdot \mathrm{NdotL} \cdot \mathrm{PhotonArea}$.  

In voxel cone tracing, we store only one photon in each voxel, and we have $\displaystyle \mathrm{NeighborhoodArea} = {\mathrm{ConeBaseDiameter}}^2$ and $\displaystyle \mathrm{PhotonArea} = {\mathrm{VoxelSize}}^2$. This means that we have the approximation of the outgoing radiance at **VoxelPosition** and **VoxelOutgoingDirection** that $\displaystyle \operatorname{L_o}(\mathrm{VoxelPosition}, \mathrm{VoxelOutgoingDirection}) \approx \frac{1}{{\mathrm{ConeBaseDiameter}}^2} \cdot \operatorname{BRDF}(\mathrm{VoxelPosition}, \mathrm{VoxelOutgoingDirection}) \cdot \operatorname{E_N}(\mathrm{VoxelPosition}) \cdot {\mathrm{VoxelSize}}^2$. During the **voxelization** step, the $\displaystyle \operatorname{BRDF}(\mathrm{VoxelPosition}, \mathrm{VoxelOutgoingDirection}) \cdot \operatorname{E_N}(\mathrm{VoxelPosition})$ part of the formula is calculated and store in voxels. During the **cone tracing** step, the $\displaystyle \frac{1}{{\mathrm{ConeBaseDiameter}}^2} \cdot {\mathrm{VoxelSize}}^2$ part of the formula is calculated on the fly.  

### 1-2\. Spherical Function

By "Figure 11.1" of [Real-Time Rendering Fourth Edition](http://www.realtimerendering.com/), ["Figure 14.14"](https://pbr-book.org/3ed-2018/Light_Transport_I_Surface_Reflection/The_Light_Transport_Equation) of [PBR Book V3](https://www.pbr-book.org/3ed-2018/contents) and ["Figure 13.1"](https://www.pbr-book.org/4ed/Light_Transport_I_Surface_Reflection/The_Light_Transport_Equation) of [PBR Book V4](https://www.pbr-book.org/4ed/contents), by assuming no **participating media**, we have the relationship $\displaystyle \mathop{\mathrm{L_i}}(\overrightarrow{p}, \overrightarrow{\omega_i}) = \mathop{\mathrm{L_o}}(\mathop{\mathrm{t}}(\overrightarrow{p}, \overrightarrow{\omega_i}), -\overrightarrow{\omega_i})$ where $\displaystyle \mathop{\mathrm{t}}(\overrightarrow{p}, \overrightarrow{\omega})$ is the ray-casting function. This means that the incident radiance $\displaystyle \mathop{\mathrm{L_i}}(\overrightarrow{p}, \overrightarrow{\omega_i})$ at one position $\displaystyle \overrightarrow{p}$ is exactly the outgoing radiance $\displaystyle \mathop{\mathrm{L_o}}(\mathop{\mathrm{t}}(\overrightarrow{p}, \overrightarrow{\omega_i}), -\overrightarrow{\omega_i})$ at another position $\displaystyle \mathop{\mathrm{t}}(\overrightarrow{p}, \overrightarrow{\omega_i})$.  

In voxel cone tracing, we have $\displaystyle \mathop{\mathrm{L_i}}(\mathrm{ConeApexPosition}, \mathrm{ConeDirection}) = \mathop{\mathrm{L_o}}(\mathrm{VoxelPosition}, -\mathrm{ConeDirection})$. The **−ConeDirection** is arbitrary but only a limited number of **VoxelOutgoingDirection**s can be stored in each voxel. At this moment, we store 6 **VoxelOutgoingDirection**s in each voxel, and these directions will be treated as the 3x3 octahedral map when we reconstruct the arbitrary **−ConeDirection**.  

TODO: **Spherical Gaussians**  

## 2\. Voxelization  

### 2-1\. View Direction

By \[Takeshige 2015\], we should select the view direction based on the maximum component of the absolute triangle normal to make sure that both ```ddx(voxel_coordinates_depth_direction)``` and ```ddy(voxel_coordinates_depth_direction)``` are less than 1.0 to avoid "cracks".  

The traditional implementation (e.g. \[Takeshige 2015\]) may depend on the geometry shader to calculate the normal of triangle. However, the geometry shader is actually NOT necessary. By binding the index and vertex buffers as the ```RWByteAddressBuffer```, just like how we access the vertex information based on ```RayQuery::CommittedPrimitiveIndex``` in [DXR (DirectX Raytracing)](https://microsoft.github.io/DirectX-Specs/d3d/Raytracing.html),  we can access the vertex information of the whole triangle in the vertex shader.  

![](Voxel-Cone-Tracing-1.png)  

### 2-2\. Opacity  

By \[Takeshige 2015\], the same pixel may intersect multiple voxels in view depth direction. And this is the reason why we need to enable the [MSAA](https://learn.microsoft.com/en-us/windows/win32/api/d3d11/ne-d3d11-d3d11_standard_multisample_quality_levels) to check the opacity contribution of each sample, within the same pixel, to different voxels. In practice, the [Conservative Rasterization](https://learn.microsoft.com/en-us/windows/win32/direct3d11/conservative-rasterization) is NOT necessary, and MSAA is a better alternative.  

![](Voxel-Cone-Tracing-2.png)  

### 2-3\. Premultiplied Alpha

As we state above, during voxelization, the $\displaystyle \mathrm{BRDF} \cdot \mathrm{E_N}$ part of the photon mapping formula is calculated. And then this partial formula ($\displaystyle \mathrm{C_k} = \mathrm{BRDF} \cdot \mathrm{E_N}$) will be multiplied by the voxel opacity ($\displaystyle \mathrm{A_k}$) to calculate the premultiplied alpha (\[Dunn 2014\]) color ($\displaystyle \mathrm{A_k} \mathrm{C_k}$) which is stored in voxels.  

## 3\. Cone Tracing  

### 3-1\. Monte Carlo Method

The idea of cone tracing is intrinsically to approximate the ray of **ConeDirection** by the cone, which can be considered as the average of multiple rays within the cone aperture angle.  

By sampling the PDF (Probability Density Function), just like how we calculate the ray direction in ray tracing, we can calculate the **ConeDirection** in cone tracing.  

By "20.3 Quasirandom Low-Discrepancy Sequences" of [Colbert 2007] and "13.8.2 Quasi Monte Carlo" of PBRT-V3, the low-discrepancy sequence is the better alternative than pseudo-random sequence  

  
![](Voxel-Cone-Tracing-3.png)  

By "20.4 Mipmap Filtered Samples" of \[Colbert 2007\],  we have that $\displaystyle \mathrm{ConeSolidAngle} = \min \left( \frac{1}{\text{N}} \cdot \frac{1}{\operatorname{PDF}(\mathrm{ConeDirection})}, 2 \pi \right)$. And by [Solid Angle for Cone](https://en.wikipedia.org/wiki/Solid_angle#Solid_angles_for_common_objects), we have that $\displaystyle \cos \left( \mathrm{ConeHalfAngle} \right) = 1 - \frac{\mathrm{ConeSolidAngle}}{2 \pi}$. And then, we have that $\displaystyle \mathrm{ConeRatio} = \tan \left( \mathrm{ConeHalfAngle} \right) = \frac{\sqrt{1 - \cos^2 \left( \mathrm{ConeHalfAngle} \right)}}{\cos \left( \mathrm{ConeHalfAngle} \right)}$.  

![](Voxel-Cone-Tracing-4.png)  

### 3-2\. Self Intersection  

TODO

By \[Wachter 2019\], "3.9.5 Robust Spawned Ray Origins" of [PBR Book V3](https://pbr-book.org/3ed-2018/Shapes/Managing_Rounding_Error#RobustSpawnedRayOrigins) and "6.8.6 Robust Spawned Ray Origins" of [PBR Book V4](https://pbr-book.org/4ed/Shapes/Managing_Rounding_Error#RobustSpawnedRayOrigins), we should offset the ray origin to avoid self intersection.  

### 3-3\. Iteration  

By "Figure 11.12" of [Real-Time Rendering Fourth Edition](http://www.realtimerendering.com/), the cone tracing is approximated by intersecting the scene surface with a series of spheres of which the radius is the increasing cone base radius. 

// TODO  

Beer's Law  

Under Operator 

By \[Crassin 2011\], the **under operator** is used to calculated the final color $\displaystyle \mathrm{C}_\mathrm{Final}$ and the final occlusion $\displaystyle \mathrm{A}_\mathrm{Final}$.  

By \[Dunn 2014\], we have the recursive form of the **under operator**.  
$\displaystyle \mathrm{C}_\mathrm{Final}^{0} = 0$  
$\displaystyle \mathrm{A}_\mathrm{Final}^{0} = 0$  
$\displaystyle \mathrm{C}_\mathrm{Final}^{n + 1} = \mathrm{C}_\mathrm{Final}^{n} + (1 - \mathrm{A}_\mathrm{Final}^{n}) \cdot \mathrm{C}_{n}$  
$\displaystyle \mathrm{A}_\mathrm{Final}^{n + 1} = \mathrm{A}_\mathrm{Final}^{n} + (1 - \mathrm{A}_\mathrm{Final}^{n}) \cdot \mathrm{A}_{n}$  

Actually, the explicit form of the **under operator** can be proved by mathematical induction.  
$\displaystyle \mathrm{A}_\mathrm{Final}^{n + 1} = 1 - \prod_{i = 0}^{n} \left\lparen 1 - \mathrm{A}_{i} \right\rparen$  
$\displaystyle \mathrm{C}_\mathrm{Final}^{n + 1} = \sum_{i = 0}^{n} \left\lparen \left\lparen \prod_{\mathrm{Z}_{j} \operatorname{Nearer} \mathrm{Z}_{i}} \left\lparen 1 - \mathrm{A}_{j} \right\rparen \right\rparen \cdot \mathrm{C}_{i} \right\rparen$  

## References  
\[Jensen 2001\] [Henrik Jensen. "Realistic Image Synthesis Using Photon Mapping." AK Peters 2001.](http://www.graphics.stanford.edu/papers/jensen_book/)  
\[Hachisuka 2005\] [Toshiya Hachisuka. "High-Quality Global Illumination Rendering Using Rasterization." GPU Gems 2.](https://developer.nvidia.com/gpugems/gpugems2/part-v-image-oriented-computing/chapter-38-high-quality-global-illumination)  
\[Colbert 2007\] [Mark Colbert, Jaroslav Krivanek. "GPU-Based Importance Sampling." GPU Gems 3.](https://developer.nvidia.com/gpugems/gpugems3/part-iii-rendering/chapter-20-gpu-based-importance-sampling)  
\[Crassin 2011\] [Cyril Crassin, Fabrice Neyret, Miguel Sainz, Simon Green, Elmar Eisemann. "Interactive Indirect Illumination Using Voxel Cone Tracing." SIGGRAPH 2011.](https://research.nvidia.com/publication/interactive-indirect-illumination-using-voxel-cone-tracing)  
\[Dunn 2014\] [Alex Dunn. "Transparency (or Translucency) Rendering." NVIDIA GameWorks Blog 2014.](https://developer.nvidia.com/content/transparency-or-translucency-rendering)   
\[Takeshige 2015\] [Masaya Takeshige. "The Basics of GPU Voxelization." NVIDIA GameWorks Blog 2015.](https://developer.nvidia.com/content/basics-gpu-voxelization)  
\[Heitz 2017\] [Eric Heitz. "Geometric Derivation of the Irradiance of Polygonal Lights." Technical report 2017.](https://hal.archives-ouvertes.fr/hal-01458129)  
