The following typical spherical distributions are plotted by the [GNU Octave](http://www.octave.org) which is an open source alternative to [MATLAB](https://www.mathworks.com/help/matlab/index.html).  

## NDF GGX  

```MATLAB
# user-interface roughness parameter
r = 0.5;

# Physically Based Shading at Disney
# α = r2
alpha = r * r;
alpha2 = alpha * alpha;

# H = [h_x, h_y, h_z] is the half vector, namely, the micro normal
# Usually, H is the 'm' in the NDF formulation
# And H is treated as the domain of the spherical distribution
[h_x, h_y, h_z] = sphere (256 - 1);

# H is in the tangent space where the N is (0, 0, 1)
NoH = h_z;

# https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/BRDF.ush#L318
# https://www.mathworks.com/help/matlab/matlab_prog/array-vs-matrix-operations.html
d = 1.0 + NoH .* (NoH .* alpha2 - NoH);
D_GGX = alpha2 ./ (pi .* d .* d);

# χ is the positive characteristic function
# chi = heaviside(NoH);
chi = cast (NoH > 0, class (NoH));
D_GGX = chi .* D_GGX;

# plot
# surf(D_GGX .* h_x, D_GGX .* h_y, D_GGX .* h_z);
mesh(D_GGX .* h_x, D_GGX .* h_y, D_GGX .* h_z);
axis equal;
title ("NDF GGX");
```  

![](NDF-GGX.png)  

## G1 GGX  

```MATLAB
# user-interface roughness parameter
r = 0.5;

# Physically Based Shading at Disney
# α = r2
alpha = r * r;
alpha2 = alpha * alpha;

# V = [v_x, v_y, v_z] is the outgoing direction
# Usually, V is the 'ω_o' in the G formulation
# And V is treated as the domain of the spherical distribution
[v_x, v_y, v_z] = sphere (256 - 1);

# V is in the tangent space where the N is (0, 0, 1)
NoV = v_z;

# Equation 9.37 of Real-Time Rendering Fourth Edition
a2 = NoV .* NoV ./ (alpha2 .* (1.0 - NoV .* NoV));

# The Λ function
# Equation 9.42 of Real-Time Rendering Fourth Edition  
lambda_GGX = 0.5 * (-1.0 + sqrt(1.0 + 1.0 ./ a2));

# The G1 function
# Equation 9.24 of Real-Time Rendering Fourth Edition  
G1_GGX = 1.0 ./ (1.0 + lambda_GGX);

# technically, H is the micro normal while N is the macro normal
HoV = NoV;

# χ is the positive characteristic function
# chi = heaviside(HoV);
chi = cast (HoV > 0, class (HoV));
G1_GGX = chi .* G1_GGX;

# plot
# surf(G1_GGX .* v_x, G1_GGX .* v_y, G1_GGX .* v_z);
mesh(G1_GGX .* v_x, G1_GGX .* v_y, G1_GGX .* v_z);
axis equal;
title ("G1 GGX");
```  

![](G1-GGX.png)  

## Weak White Furnace Test GGX  

```MATLAB
# user-interface roughness parameter
r = 0.5;

# Physically Based Shading at Disney
# α = r2
alpha = r * r;
alpha2 = alpha * alpha;

# V = [v_x, v_y, v_z] is the outgoing direction
# Usually, V is the 'ω_o' in the G formulation
# And V is treated as the domain of the spherical distribution
[v_x, v_y, v_z] = sphere (256 - 1);

# V is in the tangent space where the N is (0, 0, 1)
NoV = v_z;

# Equation 9.37 of Real-Time Rendering Fourth Edition
a2 = NoV .* NoV ./ (alpha2 .* (1.0 - NoV .* NoV));

# The Λ function
# Equation 9.42 of Real-Time Rendering Fourth Edition  
lambda_GGX = 0.5 * (-1.0 + sqrt(1.0 + 1.0 ./ a2));

# The G1 function
# Equation 9.24 of Real-Time Rendering Fourth Edition  
G1_GGX = 1.0 ./ (1.0 + lambda_GGX);

# L = [L_x, L_y, L_z] is the incident direction
# Usually, L is the 'ω_i' in the BRDF formulation
[L_x, L_y, L_z] = sphere (256 - 1);

# dω_i is the corresponding surface area of the unit sphere 
d_omega_i = 1;

# H = [h_x, h_y, h_z] is the half vector, namely, the micro normal
# Usually, H is the 'm' in the NDF formulation
#h_x = v_x +
```