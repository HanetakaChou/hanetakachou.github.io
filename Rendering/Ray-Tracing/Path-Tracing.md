# Path Tracing  

## Rendering Equation  

By ["14.4 The Light Transport Equation"](https://www.pbr-book.org/3ed-2018/Light_Transport_I_Surface_Reflection/The_Light_Transport_Equation) of [PBR Book V3](https://www.pbr-book.org/3ed-2018/contents) and ["13.1 The Light Transport Equation"](https://www.pbr-book.org/4ed/Light_Transport_I_Surface_Reflection/The_Light_Transport_Equation) of [PBR Book V4](https://www.pbr-book.org/4ed/contents), we have the **LTE (Light Transport Equation)** (namely, the **Rendering Equation**) $\displaystyle \mathop{\mathrm{L_o}}(\overrightarrow{p}, \overrightarrow{\omega_o}) = \mathop{\mathrm{L_e}}(\overrightarrow{p}, \overrightarrow{\omega_o}) + \int_{\mathrm{S}^2} \mathop{\mathrm{f}}(\overrightarrow{p}, \overrightarrow{\omega_i}, \overrightarrow{\omega_o}) \mathop{\mathrm{L_i}}(\overrightarrow{p}, \overrightarrow{\omega_i}) | \cos \theta_i | \, d \overrightarrow{\omega_i}$.   

From the **Rendering Equation**, we can learn that the surface and the light are actually the same thing, since the light is merely the surface which is emissive. This is actually the idea of the [OSL (Open Shading Language)](https://github.com/AcademySoftwareFoundation/OpenShadingLanguage).  

It should be noted that, by "Equation \(11.2\)" of [Real-Time Rendering Fourth Edition](http://www.realtimerendering.com/), we have another version of the Rendering Equation $\displaystyle \mathop{\mathrm{L_o}}(\overrightarrow{p}, \overrightarrow{\omega_o}) = \mathop{\mathrm{L_e}}(\overrightarrow{p}, \overrightarrow{\omega_o}) + \int_{\mathrm{S}^2} \mathop{\mathrm{f}}(\overrightarrow{p}, \overrightarrow{\omega_i}, \overrightarrow{\omega_o}) \mathop{\mathrm{L_i}}(\overrightarrow{p}, \overrightarrow{\omega_i}) \max (0, \cos \theta_i ) \, d \overrightarrow{\omega_i}$. 

The $\displaystyle \mathop{\mathrm{f}} (\overrightarrow{p}, \overrightarrow{\omega_i}, \overrightarrow{\omega_o})$ by [Real-Time Rendering Fourth Edition](http://www.realtimerendering.com/) denotes the **BRDF (Bidirectional Reflectance Distribution Function)** where $\displaystyle \overrightarrow{\omega_o}$ and $\displaystyle \overrightarrow{\omega_i}$ must be in the same hemisphere, and this is the reason why the $\displaystyle \max (0, \cos \theta_i )$ is used.  

But the $\displaystyle \mathop{\mathrm{f}} (\overrightarrow{p}, \overrightarrow{\omega_i}, \overrightarrow{\omega_o})$ by [PBR Book](https://www.pbr-book.org) denotes the **BSDF (Bidirectional Scattering Distribution Function)** (namely, $\displaystyle \left( \mathop{\mathrm{BSDF}} (\overrightarrow{p}, \overrightarrow{\omega_i}, \overrightarrow{\omega_o}) = \begin{cases} \mathop{\mathrm{BRDF}} (\overrightarrow{p}, \overrightarrow{\omega_i}, \overrightarrow{\omega_o}) & \overrightarrow{\omega_o} \text{ and }\overrightarrow{\omega_o} \text{ same hemisphere} \\ \mathop{\mathrm{BTDF}} (\overrightarrow{p}, \overrightarrow{\omega_i}, \overrightarrow{\omega_o}) & \overrightarrow{\omega_o} \text{ and }\overrightarrow{\omega_o} \text{ NOT same hemisphere} \end{cases} \right)$), and this is the reason why the $\displaystyle | \cos \theta_i |$ is used. The BSDF is calculated by [BSDF::f](https://pbr-book.org/3ed-2018/Materials/BSDFs) of [PBR Book V3](https://www.pbr-book.org/3ed-2018/contents) and []() of [PBR Book V4](https://www.pbr-book.org/4ed/contents).   

By "Figure 11.1" of [Real-Time Rendering Fourth Edition](http://www.realtimerendering.com/), ["Figure 14.14"](https://pbr-book.org/3ed-2018/Light_Transport_I_Surface_Reflection/The_Light_Transport_Equation) of [PBR Book V3](https://www.pbr-book.org/3ed-2018/contents) and ["Figure 13.1"](https://www.pbr-book.org/4ed/Light_Transport_I_Surface_Reflection/The_Light_Transport_Equation) of [PBR Book V4](https://www.pbr-book.org/4ed/contents), by assuming no **participating media**, we have the relationship $\displaystyle \mathop{\mathrm{L_i}}(\overrightarrow{p}, \overrightarrow{\omega_i}) = \mathop{\mathrm{L_o}}(\mathop{\mathrm{r}}(\overrightarrow{p}, \overrightarrow{\omega_i}), -\overrightarrow{\omega_i})$ where $\displaystyle \mathop{\mathrm{r}}(\overrightarrow{p}, \overrightarrow{\omega})$ is the ray-casting function. This means that the incident radiance $\displaystyle \mathop{\mathrm{L_i}}(\overrightarrow{p}, \overrightarrow{\omega_i})$ at one point p is exactly the exitant radiance $\displaystyle \mathop{\mathrm{L_o}}(\mathop{\mathrm{r}}(\overrightarrow{p}, \overrightarrow{\omega_i}), -\overrightarrow{\omega_i})$ at another point $\displaystyle \mathop{\mathrm{r}}(\overrightarrow{p}, \overrightarrow{\omega_i})$.  
![](Path-Tracing-1.png)  

Hence, both the incident radiance $\displaystyle \operatorname{L_i}(\overrightarrow{p}, \overrightarrow{\omega})$ and the exitant radiance $\displaystyle \operatorname{L_o}(\overrightarrow{p}, \overrightarrow{\omega})$ can be represented by the same function $\displaystyle \operatorname{L}(\overrightarrow{p}, \overrightarrow{\omega})$. And thus, we have $\displaystyle \operatorname{L}(\overrightarrow{p}, \overrightarrow{\omega_o}) = \operatorname{L_e}(\overrightarrow{p}, \overrightarrow{\omega_o}) + \int_{\mathrm{S}^2} \operatorname{f}(\overrightarrow{p}, \overrightarrow{\omega_i}, \overrightarrow{\omega_o}) \operatorname{L}(\operatorname{r}(\overrightarrow{p}, \overrightarrow{\omega_i}), -\overrightarrow{\omega_i}) (\cos \theta_i)^+ \, d \overrightarrow{\omega_i}$ which is a **integral equation** of which the unknown function is the $\displaystyle \operatorname{L}(\overrightarrow{p}, \overrightarrow{\omega})$.  

Thus, the problem of rendering is essentially the problem of solving the integral equation. There are two independent approaches: **ray tracing** (based on the **Fredholm theory**) and **radiosity** (based on the **FEM(Finite Element Method)**).  

By ["Light transport and the rendering equation"](http://www-graphics.stanford.edu/courses/cs348b-96/transport/transport.html) of [CS 348B - Computer Graphics: Image Synthesis Techniques - Levoy 1996](http://www-graphics.stanford.edu/courses/cs348b-96/), this intergral equation is actually the [**Fredholm  integral equation of the second kind**](https://en.wikipedia.org/wiki/Fredholm_integral_equation) of which the solution is the **Liouville–Neumann series** $\displaystyle  \operatorname{L}(\overrightarrow{p_1} \rightarrow \overrightarrow{p_0}) = \operatorname{L_e} (\overrightarrow{p_1} \rightarrow \overrightarrow{p_0}) + \int_{\mathrm{S}^2} \operatorname{L_e}(\overrightarrow{p_2} \rightarrow \overrightarrow{p_1})$. 

## Throughput

## Delta Distribution  

["14.4.5 Delta Distributions in the Integrand"](https://pbr-book.org/3ed-2018/Light_Transport_I_Surface_Reflection/The_Light_Transport_Equation#DeltaDistributionsintheIntegrand) of "PBR Book V3"  
["13.1.5 Delta Distributions in the Integrand"](https://pbr-book.org/4ed/Light_Transport_I_Surface_Reflection/The_Light_Transport_Equation#DeltaDistributionsintheIntegrand) of "PBR Book V4"

## Texture Sampling and Antialiasing  

### Ray Differentials  

ray differentials -> mipmap Level   
"10.1 Texture Sampling and Antialiasing" of "PBR Book V4"  
"10.1 Sampling and Antialiasing" of "PBR Book V3"  

### Specular Antialiasing  

Toksvig   
normal variance  
the NDF of the average normal and the average roughness (separately) is NOT the average NDF  
[NormalCurvatureToRoughness](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/BasePassPixelShader.usf#L67) of "Unreal Engine"  
[TextureNormalVariance](https://github.com/Unity-Technologies/Graphics/blob/v10.8.1/com.unity.render-pipelines.core/ShaderLibrary/CommonMaterial.hlsl#L214) of "Unity3D"  
"7.8.1 Mipmapping BRDF and Normal Maps" of "Real-Time Rendering Third Edition"  
"9.13.1 Filtering Normals and Normal Distributions" of "Real-Time Rendering Fourth Edition"  
