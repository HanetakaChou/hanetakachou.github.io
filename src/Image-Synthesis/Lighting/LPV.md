# LPV (Light Propagation Volumes)  

## SH (Spherical Harmonics)  

Let $\displaystyle \operatorname{\Upsilon_l^m}(\overrightarrow{\omega})$ be the SH basis function of which l is the degree (band) and m is the basis function index from -l to l.  

By "Appendix A2" of \[Sloan 2008\], we have the **polynomial forms** of SH basis $\displaystyle \operatorname{\Upsilon_l^m}(\overrightarrow{\omega})$. These polynomial forms are calculated by [sh_eval_basis_1](https://github.com/microsoft/DirectXMath/blob/jul2018b/SHMath/DirectXSH.cpp#L105) in DirectXMath, and [SHBasisFunction](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/SHCommon.ush#L215) in UE4.  

Note that the direction vector $\displaystyle \begin{bmatrix} x & y & z\end{bmatrix}$ should be **normalized** before using the polynomial forms. By "13.5.3 Spherical Coordinates" of [PBRT-V3](https://pbr-book.org/3ed-2018/Monte_Carlo_Integration/Transforming_between_Distributions#SphericalCoordinates), we have $\displaystyle \begin{bmatrix} x & y & z\end{bmatrix} = \begin{bmatrix} \sin \theta \cos \phi & \sin \theta \sin \phi & \cos \theta \end{bmatrix}$ where $\displaystyle \phi$ is the azimuth and $\displaystyle \theta$ is the inclination (in physics, while in mathmatics $\displaystyle \theta$ is the azimuth and $\displaystyle \phi$ is the inclination).  

l  |  m  | $\displaystyle \operatorname{\Upsilon_l^m}(\overrightarrow{\omega})$  
:-: | :-: | :-:  
0  |  0  | $\displaystyle \frac{1}{2 \sqrt{\pi}} = 0.282094791773878140$       
1  | -1  | $\displaystyle - \frac{\sqrt{3}}{2 \sqrt{\pi}} y = -0.488602511902919920 y$     
1  |  0  | $\displaystyle \frac{\sqrt{3}}{2 \sqrt{\pi}} z = 0.488602511902919920 z$     
1  |  1  | $\displaystyle - \frac{\sqrt{3}}{2 \sqrt{\pi}} x = -0.488602511902919920 x$     


Let $\displaystyle \operatorname{\mathcal{SH}}$ be the **SH (Spherical Harmonics) projection operation**. Analogous to the **Fourier transform**, we have $\displaystyle k_l^m = \operatorname{\mathcal{SH}}(\operatorname{f}(\overrightarrow{\omega})) = \int_{\mathrm{S}^2} \operatorname{f}(\overrightarrow{\omega}) \operatorname{\Upsilon_l^m}(\overrightarrow{\omega}) \, d\overrightarrow{\omega}$, and the original function can be reconstructed as the SH series $\displaystyle\operatorname{f}(\overrightarrow{\omega}) = \sum k_l^m \operatorname{\Upsilon_l^m}(\overrightarrow{\omega})$.  

Let R be the rotation matrix, and we have $\displaystyle {k'}_l^m = \operatorname{\mathcal{SH}}(\operatorname{f}(\mathrm{R} \overrightarrow{\omega})) = \int_{\mathrm{S}^2} \operatorname{f}(\mathrm{R} \overrightarrow{\omega}) \operatorname{\Upsilon_l^m}(\overrightarrow{\omega}) \, d\overrightarrow{\omega}$. By "Appendix: SH Rotation" of \[Kautz 2002\], we have the **rotational invariance** $\displaystyle \begin{bmatrix} {k'}_l^{-l} \\ \vdots \\ {k'}_l^0 \\ \vdots \\ {k'}_l^l \end{bmatrix} = \mathrm{M}_l \begin{bmatrix} k_l^{-l} \\ \vdots \\ k_l^0 \\ \vdots \\ k_l^l \end{bmatrix}$ where $\displaystyle \mathrm{M}_l^{ij} = \int_{\mathrm{S}^2} \operatorname{\Upsilon_l^{i - l}}(\mathrm{R} \overrightarrow{\omega}) \operatorname{\Upsilon_l^{j - l}}(\overrightarrow{\omega}) \, d\overrightarrow{\omega}$.  

l | i | j | $\displaystyle \mathrm{M}_l^{ij}$  
:-: | :-: | :-: | :-:  
0 | 0 | 0 | $\displaystyle \mathrm{M}_0^{00} = \int_{\mathrm{S}^2} \operatorname{\Upsilon_0^0}(\mathrm{R} \overrightarrow{\omega}) \operatorname{\Upsilon_0^0}(\overrightarrow{\omega}) \, d\overrightarrow{\omega} = \int_{\mathrm{S}^2} \frac{1}{2 \sqrt{\pi}} \frac{1}{2 \sqrt{\pi}} \, d\overrightarrow{\omega} = \frac{1}{4\pi} \int_{\mathrm{S}^2} 1 \, d\overrightarrow{\omega} = \frac{1}{4\pi} 4\pi = 1$  
1 | 0 | 0| $\displaystyle \mathrm{M}_1^{00} = \int_{\mathrm{S}^2} \operatorname{\Upsilon_1^{-1}}(\mathrm{R} \overrightarrow{\omega}) \operatorname{\Upsilon_1^{-1}}(\overrightarrow{\omega}) \, d\overrightarrow{\omega} = $  
   
[XMSHRotate](https://github.com/microsoft/DirectXMath/blob/jul2018b/SHMath/DirectXSH.cpp#L1026)  

[XMSHRotateZ](https://github.com/microsoft/DirectXMath/blob/jul2018b/SHMath/DirectXSH.cpp#L1163)  

// Analytic Models

[XMSHEvalConeLight](https://github.com/microsoft/DirectXMath/blob/jul2018b/SHMath/DirectXSH.cpp#L4664)

// Appendix A3 ZH Coefficients for Spherical Light Source  

The light position is at the Z axis  

![](LPV-1.png)  

 

By "13.5.3 Spherical Coordinates" of [PBRT-V3](https://pbr-book.org/3ed-2018/Monte_Carlo_Integration/Transforming_between_Distributions#SphericalCoordinates), we have $\displaystyle \int_{\Omega} \operatorname{\Upsilon_l^0}(\overrightarrow{\omega}) \, d \overrightarrow{\omega} = \int_0^{2\pi} \left\lparen \int_0^{\alpha} \operatorname{\Upsilon_l^0}(\overrightarrow{\omega}) \sin \theta \, d \theta \right\rparen \, d \phi$.  

For l = 0, we have $\operatorname{\Upsilon_0^0}(\overrightarrow{\omega}) = \frac{1}{2 \sqrt{\pi}}$ and $\displaystyle \int_{\Omega} \operatorname{\Upsilon_0^0}(\overrightarrow{\omega}) \, d \overrightarrow{\omega} = \int_{\Omega} \frac{1}{2 \sqrt{\pi}} \, d \overrightarrow{\omega} = \frac{1}{2 \sqrt{\pi}} \int_{\Omega} 1 \, d \overrightarrow{\omega} = \frac{1}{2 \sqrt{\pi}} \int_0^{2\pi} \left\lparen \int_0^{\alpha} \sin \theta \, d \theta \right\rparen \, d \phi = \frac{1}{2 \sqrt{\pi}} \int_0^{2\pi} ( (-\cos \alpha) - (-\cos 0) ) \, d \phi = \frac{1}{2 \sqrt{\pi}} 2\pi ( (-\cos \alpha) - (-\cos 0) ) = -\sqrt{\pi} (-1 + \cos \alpha)$.  

For l = 1, we have $\operatorname{\Upsilon_1^0}(\overrightarrow{\omega}) = \frac{\sqrt{3}}{2 \sqrt{\pi}} z$ and $\displaystyle \int_{\Omega} \operatorname{\Upsilon_1^0}(\overrightarrow{\omega}) \, d \overrightarrow{\omega} = \int_{\Omega} \frac{\sqrt{3}}{2 \sqrt{\pi}} z \, d \overrightarrow{\omega} = \frac{\sqrt{3}}{2 \sqrt{\pi}} \int_{\Omega} z \, d \overrightarrow{\omega} = \frac{\sqrt{3}}{2 \sqrt{\pi}} \int_0^{2\pi} \left\lparen \int_0^{\alpha} z \sin \theta \, d \theta \right\rparen \, d \phi = \frac{\sqrt{3}}{2 \sqrt{\pi}} \int_0^{2\pi} \left\lparen \int_0^{\alpha} \cos \theta \sin \theta \, d \theta \right\rparen \, d \phi = \frac{\sqrt{3}}{2 \sqrt{\pi}} \int_0^{2\pi} \left\lparen \frac{\sin^2 \alpha}{2} - \frac{\sin^2 0}{2} \right\rparen \, d \phi = \frac{\sqrt{3}}{2 \sqrt{\pi}} 2\pi \frac{\sin^2 \alpha}{2} = \frac{1}{2} \sqrt{3} \sqrt{\pi} \sin^2 \alpha$.  

## References  
\[Kautz 2002\] [Jan Kautz, Peter-Pike Sloan, John Snyder. "Fast, Arbitrary BRDF Shading for Low-Frequency Lighting Using Spherical Harmonics." EGWR 2002.](http://www.ppsloan.org/publications/shbrdf_final17.pdf)  
\[Sloan 2008\] [Peter-Pike Sloan. "Stupid Spherical Harmonics (SH) Tricks." GDC 2008.](http://www.ppsloan.org/publications/StupidSH36.pdf)  
\[Kaplanyan 2009\] [Anton Kaplanyan. "Light Propagation Volumes in CryEngine 3." SIGGRAPH 2009.](https://advances.realtimerendering.com/s2009/Light_Propagation_Volumes.pdf)  
\[Kaplanyan 2010\] Anton Kaplanyan. "Cascaded Light Propagation Volumes for Real-Time Indirect Illumination." I3D 2010.  
\[Kaplanyan 2011\] Anton Kaplanyan, Wolfgang Engel, Carsten Dachsbacher. "Diffuse Global Illumination with Temporally Coherent Light Propagation Volumes." GPU Pro 2.  
\[Engel 2012\] Wolfgang Engel, Igor Lobanchikov, Timothy Martin. "Dynamic Global Illumination from Many Lights." AltDevConf 2012.  
