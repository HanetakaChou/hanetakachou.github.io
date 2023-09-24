# Dual Paraboloid Mapping

## Definition  

Let the equation of the **(elliptic) paraboloid** be $\displaystyle z = \frac{1}{2} - \frac{1}{2}(x^2 + y^2)$.  

Evidently, the plane section of this paraboloid is the **parabola** of which the **focus** is the origin, the **vertex** is $\displaystyle (0, 0, \frac{1}{2})$ and the **directrix** is $\displaystyle z = 1$.  
Proof:  
For example, let $\displaystyle y = 0$, we have the intersection of the paraboloid and ZOX plane $\displaystyle z = \frac{1}{2} - \frac{1}{2} x^2$ which can be obtained by translating parabola $\displaystyle z = - \frac{1}{2} x^2$ by $\displaystyle \frac{1}{2}$ units in the positive Z direction.  
And the parabola $\displaystyle z = - \frac{1}{2} x^2$ can be written as $\displaystyle x^2 = -2z$. Compared to the standard equation $\displaystyle x^2 = -2pz$, we have **semi-latus rectum** $\displaystyle p = 1$. This means that $\displaystyle z = - \frac{1}{2} x^2$ is the parabola of which the focus is the $\displaystyle (0, 0, -\frac{p}{2}) = (0, 0, -\frac{1}{2})$, the vertex is the origin and the directrix is $\displaystyle z = \frac{p}{2} = \frac{1}{2}$.  
And we translate parabola $\displaystyle z = - \frac{1}{2} x^2$ by $\displaystyle \frac{1}{2}$ units in the positive Z direction to obtain $\displaystyle z = \frac{1}{2} - \frac{1}{2} x^2$ of which the focus is the origin $\displaystyle (0, 0, -\frac{p}{2} + \frac{1}{2}) = (0, 0, 0)$, the vertex is $\displaystyle (0, 0, 0 + \frac{1}{2}) = (0, 0, \frac{1}{2})$ and the directrix is $\displaystyle z = \frac{1}{2} + \frac{1}{2} = 1$.  

Let $\displaystyle \overrightarrow{(\text{x\_norm}, \text{y\_norm}, \text{z\_norm})}$ be one of the directions in the domain of the spherical function. The goal of the paraboloid mapping is to transform this direction to the 2D texture coordinate $\displaystyle (\text{x\_2d}, \text{y\_2d})$.  
Proof:  
![](Dual-Paraboloid-Mapping-1.png)  
Let the ray from focus F with direction $\displaystyle \overrightarrow{(\text{x\_norm}, \text{y\_norm}, \text{z\_norm})}$ intersect the paraboloid at point P. Evidently, the unit vector in the direction of $\displaystyle \overrightarrow{FP}$ is $\displaystyle \overrightarrow{(\text{x\_norm}, \text{y\_norm}, \text{z\_norm})}$.  
Let PM be the **perpendicular distance** from P to directrix $\displaystyle z = 1$. Evidently, the unit vector in the the direction of $\displaystyle \overrightarrow{PM}$ is $\displaystyle \overrightarrow{(0, 0, 1)}$. And we have $\displaystyle \overrightarrow{FM} = \overrightarrow{FH} + \overrightarrow{HM} = \overrightarrow{(0, 0, 1)} + \overrightarrow{(\text{x\_2d}, \text{y\_2d}, 0)} = \overrightarrow{(\text{x\_2d}, \text{y\_2d}, 1)}$.  
Let $\displaystyle \overrightarrow{PN}$ be the angle bisector of $\displaystyle \overrightarrow{FP}$ and $\displaystyle \overrightarrow{PM}$. And we have the direction of $\displaystyle \overrightarrow{PN}$ is that $\displaystyle \overrightarrow{(\text{x\_norm}, \text{y\_norm}, \text{z\_norm})} + \overrightarrow{(0, 0, 1)} = \overrightarrow{(\text{x\_norm}, \text{y\_norm}, \text{z\_norm} + 1)}$.  
By the definition of the parabola, we have $\displaystyle | \overrightarrow{PM} | = | \overrightarrow{PF} |$ and thus $\displaystyle \triangle PMF$ is the **isosceles triangle**. This means that $\displaystyle \angle NPM = \angle FMP$. Hence, we have $\displaystyle \overrightarrow{PN} \parallel \overrightarrow{FM}$. This means that $\displaystyle \overrightarrow{PN} = \lambda \displaystyle \overrightarrow{FM} \Rightarrow \overrightarrow{(\text{x\_norm}, \text{y\_norm}, \text{z\_norm} + 1)} = \lambda \overrightarrow{(\text{x\_2d}, \text{y\_2d}, 1)} \Rightarrow (\text{x\_2d}, \text{y\_2d}) = \frac{1}{\text{z\_norm} + 1} (\text{x\_norm}, \text{y\_norm})$.  

// z < 0  

## Texel Solid Angle  

By "10.4.4 Other Projections" of Real-Time Rendering Fourth Edition, the texel of the dual paraboloid map is more uniform than the cube map. By "20.4.1 Mapping and Distortion" of \[Colbert 2007\], the solid angle subtended by the texel of the dual paraboloid map is $\displaystyle d\omega = \pi{(|z| + 1)}^2$.  

```MATLAB  
% here is the MATLAB code which verifies the meaning of "d_omega = (abs(z) + 1)*(abs(z) + 1)".

% "13.6.2 Sampling a Unit Disk" of [PBR Book](https://pbr-book.org/).
xi_1_size = 4096.0;
xi_2_size = 4096.0;
[ xi_1, xi_2 ] = meshgrid(linspace(0.0, 1.0, xi_1_size), linspace(0.0, 1.0, xi_2_size));
r = sqrt(xi_1);
theta = 2.0 .* pi .* xi_2;
u = r .* cos(theta);
v = r .* sin(theta);

% paraboloid
x = u;
y = v;
z = 0.5 - 0.5 .* (x .* x + y .* y);

% sphere
length = sqrt(x .* x + y .* y + z .* z);
x = x ./ length;
y = y ./ length;
z = z ./ length;

% "20.4.1 Mapping and Distortion" of [GPU Gems 3](https://developer.nvidia.com/gpugems/gpugems3).
d_omega = pi .* (z + 1.0) .* (z + 1.0);

% "numerical_omega" and "groundtruth_omega" are expected to be the same.
sum_numerator = sum(sum(d_omega));
sum_denominator = xi_1_size .* xi_2_size;
numerical_omega = sum_numerator ./ sum_denominator;

groundtruth_omega = 2.0 .* pi;

% output: "numerical:6.283569 groundtruth:6.283185".
printf("numerical:%f groundtruth:%f\n", numerical_omega, groundtruth_omega);
```  

```MATLAB  
% here is the MATLAB code which verifies the meaning of "fWt = 4/(sqrt(fTmp)*fTmp)".

% "13.3.2 The Rejection Method" of [PBR Book](https://pbr-book.org/)
u_size = 4096.0;
v_size = 4096.0;
[ u, v ] = meshgrid(linspace(-1.0, 1.0, u_size), linspace(-1.0, 1.0, v_size));
r_2 = u .* u + v.* v;
chi = cast (r_2 < 1.0, class (r_2));

% paraboloid
x = u;
y = v;
z = 0.5 - 0.5 .* (x .* x + y .* y);

% sphere
length = sqrt(x .* x + y .* y + z .* z);
x = x ./ length;
y = y ./ length;
z = z ./ length;

% "20.4.1 Mapping and Distortion" of [GPU Gems 3](https://developer.nvidia.com/gpugems/gpugems3)  
d_omega = pi * (z + 1.0) .* (z + 1.0);

% "numerical_omega" and "groundtruth_omega" are expected to be the same.
sum_numerator = sum(sum(chi .* d_omega));
sum_denominator = sum(sum(chi .* 1.0));
numerical_omega = sum_numerator ./ sum_denominator;

groundtruth_omega = 2.0 .* pi;

% output: "numerical:6.283235 groundtruth:6.283185".
printf("numerical:%f groundtruth:%f\n", numerical_omega, groundtruth_omega);
```  

## Perspective-Correct Interpolation

![](Dual-Paraboloid-Mapping-2.png)  
![](Dual-Paraboloid-Mapping-3.png)  
![](Dual-Paraboloid-Mapping-4.png)  
![](Dual-Paraboloid-Mapping-5.png)  

## References  
\[Heidrich 1998\] Wolfgang Heidrich, Hans-Peter Seidel. "View-independent Environment Maps." EGSR 1998.  
\[Colbert 2007\] [Mark Colbert, Jaroslav Krivanek. "GPU-Based Importance Sampling." GPU Gems 3.](https://developer.nvidia.com/gpugems/gpugems3/part-iii-rendering/chapter-20-gpu-based-importance-sampling)  
\[Imagination 2017\] [Imagination. "Dual Paraboloid Environment Mapping." Power SDK Whitepaper 2017.](https://github.com/powervr-graphics/Native_SDK/blob/R17.1-v4.3/Documentation/Whitepapers/Dual%20Paraboloid%20Environment%20Mapping.Whitepaper.pdf)  
