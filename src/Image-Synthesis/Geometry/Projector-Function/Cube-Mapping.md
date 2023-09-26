# Cube Mapping  

## Texel Solid Angle  

Actually, the texel of the cube map is NOT uniform. This means that the solid angle subtended by each texel of the cube map is NOT the same. Let u and v be the texcoord of the cube map. By "Equation \(5.6\)" of [PBRT-V3](https://pbr-book.org/3ed-2018/Color_and_Radiometry/Working_with_Radiometric_Integrals#IntegralsoverArea), we have $\displaystyle d\omega = \frac{dA \cos \theta}{r^2} = dA \cdot \cos \theta \cdot \frac{1}{r^2} = \frac{(1 - (-1)) \cdot (1 - (-1))}{\text{cubesize\_u} \cdot \text{cubesize\_v}} \cdot \frac{1}{\sqrt{1^2 + u^2 +v^2}} \cdot \frac{1}{1^2 + u^2 +v^2} = \frac{1}{\text{cubesize\_u} \cdot \text{cubesize\_v}} \cdot \frac{4}{\sqrt{1^2 + u^2 +v^2} \cdot (1^2 + u^2 +v^2)}$. Actually the pseudo code "fWt = 4/(sqrt(fTmp)*fTmp)" by "Projection from Cube Maps" of \[Sloan 2008\] is exactly the $\displaystyle \frac{4}{\sqrt{1^2 + u^2 +v^2} \cdot (1^2 + u^2 +v^2)}$. The common divisor $\displaystyle \frac{1}{\text{cubesize\_u} \cdot \text{cubesize\_v}}$ can be reduced, and thus is NOT calculated by \[Sloan 2008\]. The solid angle is calculated by [SHProjectCubeMap](https://github.com/microsoft/DirectXMath/blob/jul2018b/SHMath/DirectXSHD3D11.cpp#L341) in DirectXMath and [DiffuseIrradianceCopyPS](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/ReflectionEnvironmentShaders.usf#L448) in UE4.  

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
## References  
\[Sloan 2008\] [Peter-Pike Sloan. "Stupid Spherical Harmonics (SH) Tricks." GDC 2008.](http://www.ppsloan.org/publications/StupidSH36.pdf)  
