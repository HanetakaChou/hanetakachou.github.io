
## SH (Spherical Harmonics)  

### Polynomial Forms

We merely focus on the polynomial forms by "[Sloan 2008] / Appendix A2 Polynomial Forms of SH Basis".  
 i  |  l  |  m  | P  
:-: | :-: | :-: | :-  
 0  |  0  |  0  | 0.282094791773878140  
 1  |  1  | -1  | -0.488602511902919920\*y  
 2  |  1  |  0  | 0.488602511902919920\*z  
 3  |  1  |  1  | -0.488602511902919920\*x  
 4  |  2  | -2  | 1.092548430592079200\*x\*y  
 4  |  2  | -1  | -1.092548430592079200\*y\*z  
 4  |  2  |  0  | 0.946174695757560080\*z\*z + -0.315391565252520050  
 4  |  2  |  1  | -1.092548430592079200\*x\*z  
 4  |  2  |  2  | 0.546274215296039590\*(x\*x - y\*y)  


### Cubemap Texel Solid Angle

Let u and v be the texcoord of the cubemap, 


The pseudo-code is provided by "[Sloan 2008] / Projection from Cube Maps". According to the Equation (5.6) of the [PBR Book](https://pbr-book.org/3ed-2018/Color_and_Radiometry/Working_with_Radiometric_Integrals#IntegralsoverArea), we can comprehend that the "fWt = 4 / (sqrt(fTmp) * fTmp)" in the pseudo-code is merely to calculate the $\displaystyle d\omega$ without the common divisor "1.0 / cube_size / cube_size". And here is the MATLAB code which verifies the meaning of "fWt".  
```MATLAB
% retrieved by "textureSize(GLSL)" or "GetDimensions(HLSL)"
cube_size = 4096.0;

[ u, v ] = meshgrid(linspace(-1.0, 1.0, cube_size), linspace(-1, 1, cube_size));

% Equation (5.6) of the [PBR Book](https://pbr-book.org/3ed-2018/Color_and_Radiometry/Working_with_Radiometric_Integrals#IntegralsoverArea)
% "Stupid Spherical Harmonics (SH) Tricks" / "Projection from Cube Maps" / "fWt = 4/(sqrt(fTmp)*fTmp)"
r_2 = 1.0 .* 1.0 + u .* u + v .* v;
% the common divisor "1.0 ./ cube_size ./ cube_size" can be reduced, and thus is NOT calculated in "fWt = 4/(sqrt(fTmp)*fTmp)"
d_a = (1.0 - (-1.0)) .* (1.0 - (-1.0)) ./ cube_size ./ cube_size;
cos_theta = 1.0 ./ sqrt(r_2);
d_omega = d_a .* cos_theta ./ r_2;

% "numerical_omega" and "groundtruth_omega" are expected to be the same
numerical_omega = sum(sum(d_omega));
groundtruth_omega = 4.0 .* pi .* 1.0 .* 1.0 / 6.0;

% output: "numerical:2.093936 groundtruth:2.094395"
printf("numerical:%f groundtruth:%f\n", numerical_omega, groundtruth_omega);
```

### Projection  

### Evaluation

## Reference  

\[Sloan 2003\] [Peter-Pike Sloan. "Efficient Evaluation of Irradiance Environment Maps." ShaderX2.](https://www.realtimerendering.com/resources/shaderx/Tips_and_Tricks_with_DirectX_9.pdf)  
\[Sloan 2008\] [Peter-Pike Sloan. "Stupid Spherical Harmonics (SH)." Tricks GDC 2008.](http://www.ppsloan.org/publications/StupidSH36.pdf)  


