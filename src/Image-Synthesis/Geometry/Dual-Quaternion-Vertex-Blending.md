# Dual Quaternion Vertex Blending

## 1\. Dual Quaternion

### Notations  
$\displaystyle a$ is a real number  
$\displaystyle \overrightarrow{v}$ is a vector in 3D space  
$\displaystyle \boldsymbol{q}$ is a quaternion  
$\displaystyle \hat{a}$ is a dual number  
$\displaystyle \hat{\boldsymbol{q}}$ is a dual quaternion  

### 1-1\. Quaternion

By "Equation \(5.3\)" of [Quaternions for Computer Graphics](https://link.springer.com/book/10.1007/978-1-4471-7509-4), a quaternion can be written as $\displaystyle \boldsymbol{q} = w + xi + yj + zk = \begin{bmatrix}s, & \overrightarrow{v}\end{bmatrix}$ where $\displaystyle s = w$ is a real number and $\displaystyle \overrightarrow{v} = \begin{bmatrix}x, & y, & z\end{bmatrix}$ is a vector in 3D space.  

#### 1-1-1\. Multiplication  

By "Equation \(5.9\)" of [Quaternions for Computer Graphics](https://link.springer.com/book/10.1007/978-1-4471-7509-4), we have the quaternion multiplication $\displaystyle \boldsymbol{q_0}\boldsymbol{q_1} = \begin{bmatrix}s_0, & \overrightarrow{v_0}\end{bmatrix} \begin{bmatrix}s_1, & \overrightarrow{v_1}\end{bmatrix} = \begin{bmatrix}s_0 s_1 - \overrightarrow{v_0} \cdot \overrightarrow{v_1}, & s_0 \overrightarrow{v_1} + s_1 \overrightarrow{v_0} + \overrightarrow{v_0} \times \overrightarrow{v_1}\end{bmatrix}$.  

#### 1-1-2\. Conjugation  

By "5.12 The Conjugate" of [Quaternions for Computer Graphics](https://link.springer.com/book/10.1007/978-1-4471-7509-4), we have the quaternion conjugation ${\boldsymbol{q}}^* = {\begin{bmatrix}s, & \overrightarrow{v}\end{bmatrix}}^* = \begin{bmatrix}s, & -\overrightarrow{v}\end{bmatrix}$.  

#### 1-1-3\. Inner Product 

By "Equation \(22\)" of \[Kavan 2008\], we have that the result of $\displaystyle \boldsymbol{q_0} {\boldsymbol{q_\epsilon}}^* + \boldsymbol{q_\epsilon} {\boldsymbol{q_0}}^*$ is a real number and can be written as the [inner product](https://en.wikipedia.org/wiki/Inner_product_space#Definition) form $\displaystyle \boldsymbol{q_0} {\boldsymbol{q_\epsilon}}^* + \boldsymbol{q_\epsilon} {\boldsymbol{q_0}}^* = 2 (s_0 s_\epsilon + \overrightarrow{v_0} \cdot \overrightarrow{v_\epsilon}) = 2 (w_0 w_\epsilon + x_0 x_\epsilon + y_0 y_\epsilon + z_0 z_\epsilon) = 2 \langle \boldsymbol{q_0}, \boldsymbol{q_\epsilon} \rangle$.  

Proof  
  
> By "1-1-1\. Multiplication", we have $\displaystyle \boldsymbol{q_0} {\boldsymbol{q_\epsilon}}^* + \boldsymbol{q_\epsilon} {\boldsymbol{q_0}}^* = \begin{bmatrix}s_0, & \overrightarrow{v_0}\end{bmatrix} \begin{bmatrix}s_\epsilon, & -\overrightarrow{v_\epsilon}\end{bmatrix} + \begin{bmatrix}s_\epsilon, & \overrightarrow{v_\epsilon}\end{bmatrix} \begin{bmatrix}s_0, & -\overrightarrow{v_0}\end{bmatrix} = \begin{bmatrix}s_0 s_\epsilon - \overrightarrow{v_0} \cdot (-\overrightarrow{v_\epsilon}), & s_0 (-\overrightarrow{v_\epsilon}) + s_\epsilon \overrightarrow{v_0} + \overrightarrow{v_0} \times (-\overrightarrow{v_\epsilon})\end{bmatrix} + \begin{bmatrix}s_\epsilon s_0 - \overrightarrow{v_\epsilon} \cdot (-\overrightarrow{v_0}), & s_\epsilon (-\overrightarrow{v_0}) + s_0 \overrightarrow{v_\epsilon} + \overrightarrow{v_\epsilon} \times (-\overrightarrow{v_0})\end{bmatrix} = \begin{bmatrix} s_0 s_\epsilon - \overrightarrow{v_0} \cdot (-\overrightarrow{v_\epsilon}) + s_\epsilon s_0 - \overrightarrow{v_\epsilon} \cdot (-\overrightarrow{v_0}), & s_0 (-\overrightarrow{v_\epsilon}) + s_\epsilon \overrightarrow{v_0} + \overrightarrow{v_0} \times (-\overrightarrow{v_\epsilon}) + s_\epsilon (-\overrightarrow{v_0}) + s_0 \overrightarrow{v_\epsilon} + \overrightarrow{v_\epsilon} \times (-\overrightarrow{v_0})\end{bmatrix} = \begin{bmatrix}2 (s_0 s_\epsilon + \overrightarrow{v_0} \cdot \overrightarrow{v_\epsilon}), & \overrightarrow{0}\end{bmatrix} = 2 (s_0 s_\epsilon + \overrightarrow{v_0} \cdot \overrightarrow{v_\epsilon})$.  

#### 1-1-4\. Norm  

By "5.12 The Conjugate" of [Quaternions for Computer Graphics](https://link.springer.com/book/10.1007/978-1-4471-7509-4), we have the norm of a quaternion $\displaystyle {\| \boldsymbol{q} \|}^2 = \boldsymbol{q} {\boldsymbol{q}}^* = \begin{bmatrix}s, & \overrightarrow{v}\end{bmatrix} \begin{bmatrix}s, & -\overrightarrow{v}\end{bmatrix} = \begin{bmatrix}s^2 - \overrightarrow{v} \cdot (-\overrightarrow{v}), & s (-\overrightarrow{v}) + s \overrightarrow{v} + \overrightarrow{v} \times (-\overrightarrow{v})\end{bmatrix} = \begin{bmatrix}s^2 + {|\overrightarrow{v}|}^2, &  \overrightarrow{0}\end{bmatrix} = s^2 + {|\overrightarrow{v}|}^2 = w^2 + x^2 + y^2 + z^2 = \langle \boldsymbol{q}, \boldsymbol{q} \rangle \Rightarrow \| \boldsymbol{q} \| = \sqrt{\langle \boldsymbol{q}, \boldsymbol{q} \rangle}$.  

#### 1-1-5\. Unit Quaternion  

By "5.14 Normalised Quaternion" of [Quaternions for Computer Graphics](https://link.springer.com/book/10.1007/978-1-4471-7509-4), a unit quaterion is a quaterion of which the norm is 1.  

#### 1-1-6\. Inverse 

By "5.16 Inverse Quaternion" of [Quaternions for Computer Graphics](https://link.springer.com/book/10.1007/978-1-4471-7509-4), we have the inverse of the quaternion $\displaystyle \boldsymbol{q} {\boldsymbol{q}}^{-1} = 1 = \begin{bmatrix}1, &  \overrightarrow{0}\end{bmatrix} \Rightarrow {\boldsymbol{q}}^* \boldsymbol{q} {\boldsymbol{q}}^{-1} = {\boldsymbol{q}}^* \Rightarrow ({\boldsymbol{q}}^* \boldsymbol{q}) {\boldsymbol{q}}^{-1} = {\boldsymbol{q}}^* \Rightarrow {\| \boldsymbol{q} \|}^2 {\boldsymbol{q}}^{-1} = {\boldsymbol{q}}^* \Rightarrow {\boldsymbol{q}}^{-1} = \frac{{\boldsymbol{q}}^*}{{\| \boldsymbol{q} \|}^2}$.  

#### 1-1-7\. Bijection between Rotation Transformations and Unit Quaternions  

Each rotation transformation can be represented by a unit quaternion. And conversely, each unit quaternion can represent a rotation transformation.  

#### 1-1-7-1\. Bijection between [axis, angle] and Unit Quaternion

Let $\displaystyle \boldsymbol{p} = \begin{bmatrix}0, & \overrightarrow{p}\end{bmatrix}$ be the position in 3D space.  

Evidently, each unit quaternion can be written as $\displaystyle \boldsymbol{q} = \begin{bmatrix}\cos \frac{\theta}{2}, & \sin \frac{\theta}{2} \overrightarrow{n}\end{bmatrix}$ where $\displaystyle \overrightarrow{n}$ is a unit vector in 3D space.   

By "1-1-6\. Inverse", we have $\displaystyle {\boldsymbol{q}}^{-1} = \frac{\begin{bmatrix}\cos \frac{\theta}{2}, & - \sin \frac{\theta}{2} \overrightarrow{n}\end{bmatrix}}{{\| \boldsymbol{q} \|}^2} = \begin{bmatrix}\cos \frac{\theta}{2}, & - \sin \frac{\theta}{2} \overrightarrow{n}\end{bmatrix}$  
 
By "1-1-1\. Multiplication", we have $\displaystyle \boldsymbol{p'} = \boldsymbol{q} \boldsymbol{p} {\boldsymbol{q}}^{-1} = \begin{bmatrix}\cos \frac{\theta}{2}, & \sin \frac{\theta}{2} \overrightarrow{n}\end{bmatrix} \begin{bmatrix}0, & \overrightarrow{p}\end{bmatrix} \begin{bmatrix}\cos \frac{\theta}{2}, & - \sin \frac{\theta}{2} \overrightarrow{n}\end{bmatrix} = \begin{bmatrix}0, & (1 - \cos \theta) (\overrightarrow{n} \cdot \overrightarrow{p}) \overrightarrow{p} + \cos \theta \overrightarrow{p} + \sin \theta \overrightarrow{n} \times \overrightarrow{p}\end{bmatrix}$. The lengthy calculation is provided by "Equation \(7.13\)" of [Quaternions for Computer Graphics](https://link.springer.com/book/10.1007/978-1-4471-7509-4).  

Let $\displaystyle \boldsymbol{p'} = \boldsymbol{q} \boldsymbol{p} {\boldsymbol{q}}^{-1} = [0, \overrightarrow{p'}]$ where $\displaystyle \overrightarrow{p'} = (1 - \cos \theta) (\overrightarrow{v} \cdot \overrightarrow{p}) \overrightarrow{p} + \cos 2 \theta \overrightarrow{p} + \sin 2 \theta \overrightarrow{v} \times \overrightarrow{p}$ is the position after the transform in 3D space.

By "Fig. 6.7" and "Fig. 6.8" of [Quaternions for Computer Graphics](https://link.springer.com/book/10.1007/978-1-4471-7509-4), we have  $\displaystyle \overrightarrow{p'}$ is the position where $\displaystyle \overrightarrow{p}$ is rotated about the axis $\displaystyle \overrightarrow{n}$ by the angle $\displaystyle \theta$.  

Proof  

> ![Fig. 6.7 A view of the geometry associated with rotating a point about an arbitrary axis](Dual-Quaternion-Vertex-Blending-1.png)  
> ![Fig. 6.8 A cross-section and plan view of the geometry associated with rotating a point about an arbitrary axis](Dual-Quaternion-Vertex-Blending-2.png)  
> TODO  
 
##### 1-1-7-2\. Mapping from Rotation Transformations to Unit Quaternions  

By "Conversion from rotation matrix to axis–angle" of [Rotation matrix](https://en.wikipedia.org/wiki/Rotation_matrix) in Wikipedia, we can deduce the axis and the angle from the rotation matrix. The main idea is that the axis is an eigenvector of the matrix and the angle can be deduced from trace of the rotation matrix.  

Once we have the axis and the angle, by "1-1-7-1\. Bijection between [axis, angle] and Unit Quaternion", we can have the quaternion.  

The implementation is provided by [XMQuaternionRotationMatrix](https://github.com/microsoft/DirectXMath/blob/jul2018b/Inc/DirectXMathMisc.inl#L708) of DirectXMath.  

##### 1-1-7-3\. Mapping from Unit Quaternions to Rotation Transformations  


### 1-2\. Dual Numbder    
By "A.1 Dual Numbers" of \[Kavan 2008\], a dual number can be written as $\displaystyle \hat{a} = a_0 + a_\epsilon \epsilon$, where $\displaystyle a_0$ and $\displaystyle a_\epsilon$ are real numbers, and $\displaystyle \epsilon$ is a basis such that $\displaystyle 1 \, \epsilon = \epsilon \, 1 = \epsilon$ and $\epsilon \,\epsilon = 0$.

#### 1-2-1\. Multiplication  
By "Equation \(17\)" of \[Kavan 2008\], we have the dual number multiplication $\displaystyle \hat{a} \hat{b} = (a_0 + a_\epsilon \epsilon)(b_0 + b_\epsilon \epsilon) = a_0 b_0 + (a_0 b_\epsilon + b_0 a_\epsilon) \epsilon$.  

#### 1-2-2\. Conjugation  
By "A.1 Dual Numbers" of \[Kavan 2008\], we have the dual number conjugation $\displaystyle \overline{\hat{a}} = \overline{a_0 + a_\epsilon \epsilon} = a_0 - a_\epsilon \epsilon$.  
  
### 2-3\. Square Root  
If $a_0 \gt 0$, then $\sqrt{a_0 + a_\epsilon\epsilon} = \sqrt{a_0} + \frac{a_\epsilon}{2\sqrt{a_0}}\epsilon$ (\[Kavan 2008\] / A Dual Quaternion Tutorial / A.1 Dual Numbers / Lemma 8).  
Proof:  
We assume that there exists the dual number $b_0 + b_\epsilon\epsilon$ such that $a_0 + a_\epsilon\epsilon = (b_0 + b_\epsilon\epsilon)(b_0 + b_\epsilon\epsilon)$, namely, $\sqrt{a_0 + a_\epsilon\epsilon} = b_0 + b_\epsilon\epsilon$.  
Evidently, we have $b_0b_0 = a_0$ and $2b_0b_\epsilon = a_\epsilon$. And thus, if $a_0 \gt 0$, we have $b_0 = \sqrt{a_0}$ and $b_\epsilon = \frac{a_\epsilon}{2\sqrt{a_0}}$.  

## 3\. Dual Quaternion  

By "A.2 Dual Quaternions" of [Kavan 2008\], a dual quaternion can be deemed not only a quaternion whose elements are dual numbers, but also a dual number whose elements are quaternions. This means that we have not only $\displaystyle \hat{\boldsymbol{q}} = \hat{q_w} + \hat{q_x}i + \hat{q_y}j + \hat{q_z}k$ where $\displaystyle \hat{q_w}$, $\displaystyle \hat{q_x}$, $\displaystyle \hat{q_y}$ and $\displaystyle \hat{q_z}$ are dual numbers, but also $\displaystyle \hat{\boldsymbol{q}} = \boldsymbol{q_0} + \boldsymbol{q_\epsilon}\epsilon$ where $\displaystyle \boldsymbol{q_0}$ and $\displaystyle \boldsymbol{q_\epsilon}$ are quaternions.  

### 3-1\. Multiplication  
$\displaystyle \hat{\boldsymbol{p}}\hat{\boldsymbol{q}} = (\boldsymbol{p_0} + \boldsymbol{p_\epsilon}\epsilon)(\boldsymbol{q_0} + \boldsymbol{q_\epsilon}\epsilon) = \boldsymbol{p_0}\boldsymbol{q_0} + (\boldsymbol{p_0}\boldsymbol{q_\epsilon} + \boldsymbol{p_\epsilon}\boldsymbol{q_0})\epsilon$ where $\displaystyle \boldsymbol{p_0}\boldsymbol{q_0}$, $\displaystyle \boldsymbol{p_0}\boldsymbol{q_\epsilon}$ and $\displaystyle \boldsymbol{p_\epsilon}\boldsymbol{q_0}$ follow the rule of the multiplication of two ordinary quaternions (\[Kavan 2008\] / A Dual Quaternion Tutorial / A.2 Dual Quaternions).  

### 3-2\. Conjugation

#### 3-2-1\. First Type of Conjugation - Quaternion Style  
By "A.2 Dual Quaternions" of \[Kavan 2008\], we have the quaternion style conjugation $\displaystyle {\hat{\boldsymbol{q}}}^* = {(\boldsymbol{q_0} + \boldsymbol{q_\epsilon} \epsilon)}^* = {\boldsymbol{q_0}}^* + {{\boldsymbol{q_\epsilon}}^*} \epsilon$.  

#### 3-2-2\. Second Type of Conjugation - Dual Number Style  
By "A.2 Dual Quaternions" of \[Kavan 2008\], we have the dual number style conjugation $\displaystyle \overline{\hat{\boldsymbol{q}}} = \overline{\boldsymbol{q_0} + \boldsymbol{q_\epsilon} \epsilon} = \boldsymbol{q_0} - \boldsymbol{q_\epsilon} \epsilon$.  

#### 3-2-3\. Commutative Property  
By "A.2 Dual Quaternions" of \[Kavan 2008\], since $\displaystyle \overline{{\hat{\boldsymbol{q}}}^*} = \overline{{(\boldsymbol{q_0} + \boldsymbol{q_\epsilon} \epsilon)}^*} = \overline{{\boldsymbol{q_0}}^* + {{\boldsymbol{q_\epsilon}}^*} \epsilon} = {\boldsymbol{q_0}}^* - {{\boldsymbol{q_\epsilon}}^*} \epsilon = {(\boldsymbol{q_0} - \boldsymbol{q_\epsilon} \epsilon)}^* = {(\overline{\boldsymbol{q_0} + \boldsymbol{q_\epsilon} \epsilon})}^* = {\overline{\hat{\boldsymbol{q}}}}^*$, we have $\overline{{\hat{\boldsymbol{q}}}^*} = {\overline{\hat{\boldsymbol{q}}}}^* = {\boldsymbol{q_0}}^* - {{\boldsymbol{q_\epsilon}}^*} \epsilon$.  

#### 3-2-4\. Distributive Property  

11111

### 3-3\. Norm  
By "Equation \(22\)" of \[Kavan 2008\], we have the norm of the dual qunternion $\displaystyle \| \hat{\boldsymbol{q}} \| = $.  

(\[Kavan 2008\] / A Dual Quaternion Tutorial / A.2 Dual Quaternions / Lemma 9).

### 3-3-1\. Unit Dual Quaternion  

1111111

### 3-4\. Bijection between Rigid Transformations and Unit Dual Quaternions  

called as Rigid Transformation

### 3-4-1\. Mapping from Rigid Transformations to Unit Dual Quaternions  

\[Kavan 2008\] / A.2 Dual Quaternions / Lemma 12  


## 2\. Linear Vertex Blending

## 3\. Dual Quaternion Vertex Blending


## Reference  
\[Kavan 2007\][Ladislav Kavan, Steven Collins, Jiri Zara, Carol O'Sullivan. "Skinning with Dual Quaternions." I3D 2007.](http://www.cs.utah.edu/~ladislav/kavan07skinning/kavan07skinning.html)  
\[Kavan 2008\] [Ladislav Kavan, Steven Collins, Jiri Zara, Carol O'Sullivan. "Geometric Skinning with Approximate Dual Quaternion Blending." SIGGRAPH 2008.](http://www.cs.utah.edu/~ladislav/kavan08geometric/kavan08geometric.html)  
\[NVIDIA 2008\] [NVIDIA. "Skinning with Dual Quaternions." NVIDIA Direct3D SDK 10.5 Code Samples.](https://developer.download.nvidia.com/SDK/10.5/direct3d/samples.html#QuaternionSkinning)  
\[Vince 2011\] [John Vince. "Quaternions for Computer Graphics." Springer 2011.](https://link.springer.com/book/10.1007/978-0-85729-760-0)  
