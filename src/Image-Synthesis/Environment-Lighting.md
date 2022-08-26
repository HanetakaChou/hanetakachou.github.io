## Environment Lighting

The name **environment lighting** is from "10.2 Environment Lighting" of [Real-Time Rendering Fourth Edition](https://www.realtimerendering.com/). The most important difference between environment light and global illumination is that the shading algorithm of the environment light is independent of the other positions on the surface except the shading position.  


### Diffuse Environment Lighting  

Let $\displaystyle \operatorname{L}(\omega)$ denote the infinitely distant radiance distribution. By \[Ramamoorthi 2001\], the irradiance can be calculated as $\displaystyle E(\overrightarrow{n}) = \int_{\operatorname{\Omega}(\overrightarrow{n})} \operatorname{L}(\omega) |\cos \theta| \, d \omega = \int_{\operatorname{\Omega}(\overrightarrow{n})} \operatorname{L}(\omega) |\overrightarrow{n} \cdot \overrightarrow{\omega}| \, d \omega$.  

### Specular Environment Lighting

According to "Equation (9.9)" of [Real-Time Rendering Fourth Edition](https://www.realtimerendering.com/), the DVF term is actually the HDR(hemispherical directional reflectance) $\displaystyle \operatorname{R}(\overrightarrow{v}) = \int_{\Omega} \operatorname{f}(\operatorname{\omega_l}, \operatorname{\omega_v}) |\cos \theta_l| \, d \omega_l = \int_{\Omega} \operatorname{f}(\operatorname{\omega_l}, \operatorname{\omega_v}) | \overrightarrow{(0,0,1)} \cdot \overrightarrow{\omega_l}| \, d \omega_l$. Since this integral can be calculated in the tangent space where the normal direction is (0, 0, 1), this integral is independent of the normal direction and can be determined by the view direction in tangent space alone.  
According to the "Equation (9)" of \[Karis 2013\], the Fresnel term is treated separately $\displaystyle \operatorname{R}(\overrightarrow{v}) = \int_\Omega \operatorname{DV}(\operatorname{\omega_l}, \operatorname{\omega_v})(F_0 + )$

Analogous to [LTC Fresnel Approximation](https://blog.selfshadow.com/publications/s2016-advances/s2016_ltc_fresnel.pdf) of \[Stephen 2016\], 


## References 
\[Ramamoorthi 2001\] [Ravi Ramamoorthi, Pat Hanrahan. "An Efficient Representation for Irradiance Environment Maps." SIGGRAPH 2001.](https://graphics.stanford.edu/papers/envmap/)
\[King 2005\] [Gary King. "Real-Time Computation of Dynamic Irradiance Environment Maps." GPU Gems 2.](https://developer.nvidia.com/gpugems/gpugems2/part-ii-shading-lighting-and-shadows/chapter-10-real-time-computation-dynamic)  
\[Colbert 2007\] [Mark Colbert, Jaroslav Krivanek. "GPU-Based Importance Sampling." GPU Gems 3.](https://developer.nvidia.com/gpugems/gpugems3/part-iii-rendering/chapter-20-gpu-based-importance-sampling)  
\[Karis 2013\] [Brian Karis. "Real Shading in Unreal Engine 4." SIGGRAPH 2013.](https://cdn2.unrealengine.com/Resources/files/2013SiggraphPresentationsNotes-26915738.pdf)  
\[Stephen 2016\] [Stephen Hill, Eric Heitz. "Real-Time Area Lighting: a Journey from Research to Production." SIGGRAPH 2016.](https://blog.selfshadow.com/publications/s2016-advances/)  
