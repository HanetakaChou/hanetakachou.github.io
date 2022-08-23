
## SH (Spherical Harmonics)  

As an engineer, we may merely focus on the polynomial forms ([Sloan 2008] / Appendix A2 Polynomial Forms of SH Basis).  

### Projection  

The pseudo-code is provided by "[Sloan 2008] / Projection from Cube Maps". By Equation (5.6) of the [PBR Book](https://pbr-book.org/3ed-2018/Color_and_Radiometry/Working_with_Radiometric_Integrals#IntegralsoverArea), we can comprehend that the "fWt = 4/(sqrt(fTmp)*fTmp)" in the pseudo-code is merely to calculate the $\displaystyle d\omega$ when the common divisor "1.0 / cube_dimension / cube_dimension"is reduced. And here is the MATLAB code which verifies the meaning of "fWt".  
```MATLAB
cube_dimension = 8192.0;

[u, v] = meshgrid(linspace (-1.0, 1.0, cube_dimension), linspace (-1, 1, cube_dimension));

# Equation (5.6) of the [PBR Book](https://pbr-book.org/3ed-2018/Color_and_Radiometry/Working_with_Radiometric_Integrals#IntegralsoverArea)
# "Stupid Spherical Harmonics (SH) Tricks" / "Projection from Cube Maps" / "fWt = 4/(sqrt(fTmp)*fTmp)"
r_2 = 1.0 .* 1.0 + u .* u + v .* v;
# the common divisor "1.0 ./ cube_dimension ./ cube_dimension" is reduced in "fWt = 4/(sqrt(fTmp)*fTmp)"
d_a = (1.0 - (-1.0)) .* (1.0 - (-1.0)) ./ cube_dimension ./ cube_dimension;
cos_theta = 1.0 ./ sqrt(r_2);
d_omega = d_a .* cos_theta ./ r_2;

# "int1" and "int2" are expected to be the same
numerical_omega = sum(sum(d_omega));
groundtruth_omega = 4.0 .* pi .* 1.0 .* 1.0 / 6.0;

# output: "numerical:2.094166 groundtruth:2.094395"
printf("numerical:%f groundtruth:%f\n", numerical_omega, groundtruth_omega);
```



## Reference  

[Sloan 2008] [Peter-Pike Sloan. "Stupid Spherical Harmonics (SH)." Tricks GDC 2008.](http://www.ppsloan.org/publications/StupidSH36.pdf)  


