## 1\. LTC  
 
### 1-1\. LTSD (Linearly Transformed Spherical Distribution)  
We assume that $\displaystyle \operatorname{D_o}(\omega_o)$ is the arbitrary **original distribution**, M is the linear transform matrix, and $\displaystyle \omega = \operatorname{normalize}(M \omega_o)$. The **linearly transformed spherical distribution** $\displaystyle \operatorname{D}(\omega)$ is defined as $\displaystyle \operatorname{D}(\omega) = \operatorname{D_o}(\omega_o) \frac{d\omega_o}{d\omega}$. Evidently, we have $\displaystyle \omega_o = \operatorname{normalize}(M^{-1} \omega)$. And the relationship between $\displaystyle d\omega_o$ and $\displaystyle d\omega$ is closed-form $\displaystyle \frac{d\omega_o}{d\omega} = \frac{|M^{-1}|}{{\|M^{-1}w\|}^3}$. The proof of this closed-form formula is provided in **Appendix A** of \[Heitz 2016\]. Note that $\displaystyle \omega_o$ and $\displaystyle \omega$ are **vectors** which represent the **direction**, while $\displaystyle d\omega_o$ and $\displaystyle d\omega$ are **solid angles** which represent the **area** on the **sphere surface**. By [the Equation (5.6) of the PBR Book](https://pbr-book.org/3ed-2018/Color_and_Radiometry/Working_with_Radiometric_Integrals#IntegralsoverArea), we have $\displaystyle d\omega = \frac{(A d\omega_o) \cos\theta}{r^2}$ where the A is the ratio, and the $\displaystyle A d\omega_o$ is the area subtended by the solid angle $\displaystyle d\omega$.  

### 1-2\. Clamped Cosine  
We assume that the normal direction in the tangent space is (0, 0, 1), which is called the **Median Vector** in \[Heitz 2016\]. The **clamped cosine** $\displaystyle \operatorname{D_o}(\omega_o) = \frac{1}{\pi} |\cos \theta_o| = \frac{1}{\pi} |\operatorname{dot}(\operatorname{vec3}(0,0,1), \omega_o = (x, y, z))| = \frac{1}{\pi} \max(z)$ is used as the **original distribution** $\displaystyle \operatorname{D_o}$. Evidently, by [the Figure 5.13 of the PBR Book](https://pbr-book.org/3ed-2018/Color_and_Radiometry/Working_with_Radiometric_Integrals#IntegralsoverProjectedSolidAngle), we have $\displaystyle \int_\Omega \operatorname{D_o} \, d\omega_o = \frac{1}{\pi} \int_\Omega |\cos \theta_o| \, d\omega_o = \frac{1}{\pi} \int_\Omega 1 \, d\omega^{\perp} = \frac{1}{\pi} \cdot \pi = 1$, and thus $\displaystyle \operatorname{D_o}$ is normalized.  

### 1-3\. LTC (Linearly Transformed Cosine) 
When the **clamped cosine** is used as the **original distribution** $\displaystyle \operatorname{D_o}(\omega_o)$, the corresponding **linearly transformed spherical distribution** $\displaystyle \operatorname{D}(\omega)$ is called the **linearly transformed cosine**.  

## 2\. LUT 
By [the Equation (5.9) of the PBR Book](https://pbr-book.org/3ed-2018/Color_and_Radiometry/Surface_Reflection#TheBRDF), we have $\displaystyle \operatorname{L_v}(\omega_v) = \int_{S^2} \operatorname{BRDF}(\omega_v, \omega_l) \operatorname{L_l}(\omega_l) |\cos \theta_l| \, d\omega_l$. And we try to approximate the $\displaystyle \operatorname{BRDF}(\omega_v, \omega_l)|\cos \theta_l|$ part of this formula by using the LTCs.  

### 2-1\. UV
Since the GGX BRDF is isotropic, the distribution can be determined by the outgoing direction $\displaystyle \omega_v$ (in tangent space) and the roughness $\displaystyle \alpha$, which are used as the UV of the LUT.  

### 2-2\. M
Actually, when M is the scaling transformation $\displaystyle M = \lambda I$, we have $\displaystyle \frac{d\omega_o}{d\omega} = \frac{|M^{-1}|}{{\|M^{-1}w\|}^3} = \frac{\frac{1}{{\lambda}^3}}{{(\frac{1}{\lambda})}^3} = 1$, and thus the LTSC is scale invariant. And since GGX BRDF is planar symmetry and isotropic, by \[Heitz 2016\], the M can be represented by only 4 parameters. The the inverse $\displaystyle M^{-1} = \begin{bmatrix} 1 & 0 & G \\ 0 & B & 0 \\ A & 0 & R \end{bmatrix}$, which is used when rendering, is stored in the LUT. This LUT is called the [**g_ltc_mat**](https://blog.selfshadow.com/sandbox/js/ltc_tables.js) in the **WebGL Demo** provided by \[Heitz 2016\].

### 2-3\. Norm
By [Integration by Substitution](https://en.wikipedia.org/wiki/Integration_by_substitution), we can comprehend intuitively that $\displaystyle \int_{\Omega} \operatorname{D}(\omega) \, d\omega = \int_{\Omega} \operatorname{D_o}(\omega_o) \frac{d\omega_o}{d\omega} d\omega = \int_{\Omega} \operatorname{D_o}(\omega_o) d\omega_o$. Since the **clamped cosine** is normalied, the LTC must be normalized.  However, $\displaystyle \operatorname{BRDF}(\omega_v, \omega_l)|\cos \theta_l|$ is **NOT** normalized. And thus the **norm** should be stored in the LUT to accomplish the approximation. This means that $\operatorname{D}(\omega_l) \approx \frac{\operatorname{BRDF}(\omega_v, \omega_l)|\cos \theta_l|}{\int_{\Omega} \operatorname{BRDF}(\omega_v, \omega_l)|\cos \theta_l| \, d\omega_l}$. This LUT is called the [**g_ltc_mag**](https://blog.selfshadow.com/sandbox/js/ltc_tables.js) in the **WebGL Demo** provided by \[Heitz 2016\].  

## 3\. Light

### 3-1\. Integration over Polygons
By [Integration by Substitution](https://en.wikipedia.org/wiki/Integration_by_substitution), we can comprehend intuitively that $\displaystyle \int_{P} \operatorname{D}(\omega) \, d\omega = \int_{P} \operatorname{D_o}(\omega_o) \frac{d\omega_o}{d\omega} d\omega = \int_{P_o} \operatorname{D_o}(\omega_o) d\omega_o$ where $\displaystyle P_o = M^{-1} P$. Evidently, $\displaystyle P_o = \operatorname{normalize}(M^{-1} P)$ is more consistent with $\displaystyle \omega_o = \operatorname{normalize}(M^{-1} \omega)$. However, even if the $\displaystyle M^{-1} P$ is **NOT** normalized, the area on the sphere surface subtended by the polygon remains the same. Thus, the normalize operator is **NOT** necessary.  

### 3-2\. Shading with Constant Polygonal Lights  
When the $\displaystyle \operatorname{L_l}(\omega_l)$ is assumed to be constant $\displaystyle L_l$, we have $\displaystyle \operatorname{L_v}(\omega_v) = \int_{P} \operatorname{BRDF}(\omega_v, \omega_l) \operatorname{L_l}(\omega_l) |\cos \theta_l| \, d\omega_l = L_l \int_{P} \operatorname{BRDF}(\omega_v, \omega_l) |\cos \theta_l| \, d\omega_l \approx L_l \int_{P} \mathrm{norm} \operatorname{D}(\omega_l) \, d\omega_l = L_l \cdot \mathrm{norm} \int_{P_o} \operatorname{D_o}(\omega_o) \, d\omega_o = L_l \cdot \mathrm{norm} \int_{P_o} |\cos \theta_o| \, d\omega_o = L_l \cdot \mathrm{norm} \cdot \operatorname{E}(P_o)$ where $\displaystyle P_o = M^{-1} P$.  
We assume the vertices $\displaystyle p_1$, $\displaystyle p_2$, ..., $\displaystyle p_n$ of the polygon $\displaystyle P_o$ are in the tangent space, normalized, and located in the upper hemisphere. By \[Heitz 2017\], the irradiance is closed-form $\displaystyle \operatorname{E}(P_o) = \frac{1}{2\pi} \sum_{i=1}^n \arccos(\operatorname{dot}(p_i, p_j)) \cdot \operatorname{dot}(\operatorname{normalize}(\operatorname{cross}(p_i, p_j)), \operatorname{vec3}(0, 0, 1))$ where (0, 0, 1) is the normal direction in the tangent space.  
The irradiance $\displaystyle \operatorname{E}(P_o)$ is calculated by the [**LTC_Evaluate**](https://blog.selfshadow.com/sandbox/shaders/ltc/ltc.fs) in the **WebGL Demo** provided by \[Heitz 2016\].  

## References  
\[Heitz 2016\] [Eric Heitz, Jonathan Dupuy, Stephen Hill, David Neubelt. "Real-Time Polygonal-Light Shading with Linearly Transformed Cosines." SIGGRAPH 2016.](https://eheitzresearch.wordpress.com/415-2/)  
\[Heitz 2017\] [Eric Heitz. "Geometric Derivation of the Irradiance of Polygonal Lights." Technical report 2017.](https://hal.archives-ouvertes.fr/hal-01458129)  


