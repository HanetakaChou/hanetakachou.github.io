# Dual Quaternion Vertex Blending

## 1\. Dual Quaternion

### Notations  
$\displaystyle a$ is a real number  
$\displaystyle \overrightarrow{v}$ is a vector in $\displaystyle \mathbb{R}^3$  
$\displaystyle \boldsymbol{q}$ is a quaternion  
$\displaystyle \hat{a}$ is a dual number  
$\displaystyle \hat{\boldsymbol{q}}$ is a dual quaternion  

## 1\. Quaternion

By "Equation \(5.3\)" of [Quaternions for Computer Graphics](https://link.springer.com/book/10.1007/978-1-4471-7509-4), a quaternion can be written as $\displaystyle \boldsymbol{q} = w + xi + yj + zk = \begin{bmatrix}s & \overrightarrow{v}\end{bmatrix}$ where $\displaystyle s = w$ is a real number and $\displaystyle \overrightarrow{v} = \begin{bmatrix}x & y & z\end{bmatrix}$ is a vector in $\displaystyle \mathbb{R}^3$.  

### 1-1\. Quaternion Multiplication  

By "Equation \(5.9\)" of [Quaternions for Computer Graphics](https://link.springer.com/book/10.1007/978-1-4471-7509-4), we have the quaternion multiplication $\displaystyle \boldsymbol{q_0}\boldsymbol{q_1} = \begin{bmatrix}s_0 & \overrightarrow{v_0}\end{bmatrix} \begin{bmatrix}s_1 & \overrightarrow{v_1}\end{bmatrix} = \begin{bmatrix}s_0 s_1 - \overrightarrow{v_0} \cdot \overrightarrow{v_1} & s_0 \overrightarrow{v_1} + s_1 \overrightarrow{v_0} + \overrightarrow{v_0} \times \overrightarrow{v_1} \end{bmatrix}$.  

### 1-2\. Quaternion Conjugation  

By "5.12 The Conjugate" of [Quaternions for Computer Graphics](https://link.springer.com/book/10.1007/978-1-4471-7509-4), we have the quaternion conjugation ${\boldsymbol{q}}^* = {\begin{bmatrix}s & \overrightarrow{v}\end{bmatrix}}^* = \begin{bmatrix}s & -\overrightarrow{v}\end{bmatrix}$.  

### 1-3\. Quaternion Inner Product 

By "Equation \(22\)" of \[Kavan 2008\], we have that the result of $\displaystyle \boldsymbol{q_0} {\boldsymbol{q_\epsilon}}^* + \boldsymbol{q_\epsilon} {\boldsymbol{q_0}}^*$ is a real number and can be written as the [inner product](https://en.wikipedia.org/wiki/Inner_product_space#Definition) form $\displaystyle \boldsymbol{q_0} {\boldsymbol{q_\epsilon}}^* + \boldsymbol{q_\epsilon} {\boldsymbol{q_0}}^* = 2 (s_0 s_\epsilon + \overrightarrow{v_0} \cdot \overrightarrow{v_\epsilon}) = 2 (w_0 w_\epsilon + x_0 x_\epsilon + y_0 y_\epsilon + z_0 z_\epsilon) = 2 \langle \boldsymbol{q_0}, {\boldsymbol{q_\epsilon}}^* \rangle$.  

Proof  
  
> By "1-1\. Multiplication", we have $\displaystyle \boldsymbol{q_0} {\boldsymbol{q_\epsilon}}^* + \boldsymbol{q_\epsilon} {\boldsymbol{q_0}}^* = \begin{bmatrix}s_0 & \overrightarrow{v_0}\end{bmatrix} \begin{bmatrix}s_\epsilon & -\overrightarrow{v_\epsilon}\end{bmatrix} + \begin{bmatrix}s_\epsilon & \overrightarrow{v_\epsilon}\end{bmatrix} \begin{bmatrix}s_0 & -\overrightarrow{v_0}\end{bmatrix} = \begin{bmatrix}s_0 s_\epsilon - \overrightarrow{v_0} \cdot (-\overrightarrow{v_\epsilon}) & s_0 (-\overrightarrow{v_\epsilon}) + s_\epsilon \overrightarrow{v_0} + \overrightarrow{v_0} \times (-\overrightarrow{v_\epsilon})\end{bmatrix} + \begin{bmatrix}s_\epsilon s_0 - \overrightarrow{v_\epsilon} \cdot (-\overrightarrow{v_0}) & s_\epsilon (-\overrightarrow{v_0}) + s_0 \overrightarrow{v_\epsilon} + \overrightarrow{v_\epsilon} \times (-\overrightarrow{v_0})\end{bmatrix} = \begin{bmatrix} s_0 s_\epsilon - \overrightarrow{v_0} \cdot (-\overrightarrow{v_\epsilon}) + s_\epsilon s_0 - \overrightarrow{v_\epsilon} \cdot (-\overrightarrow{v_0}) & s_0 (-\overrightarrow{v_\epsilon}) + s_\epsilon \overrightarrow{v_0} + \overrightarrow{v_0} \times (-\overrightarrow{v_\epsilon}) + s_\epsilon (-\overrightarrow{v_0}) + s_0 \overrightarrow{v_\epsilon} + \overrightarrow{v_\epsilon} \times (-\overrightarrow{v_0})\end{bmatrix} = \begin{bmatrix}2 (s_0 s_\epsilon + \overrightarrow{v_0} \cdot \overrightarrow{v_\epsilon}) & \overrightarrow{0}\end{bmatrix}$.  


### 1-4\. Norm  

### 1-3-1\. Unit Quaternion  

### 1-4\. Bijection between Rotation Transformations and Unit Quaternions  


## 2\. Dual Numbder    
By "A.1 Dual Numbers" of \[Kavan 2008\], a dual number can be written as $\displaystyle \hat{a} = a_0 + a_\epsilon \epsilon$, where $\displaystyle a_0$ and $\displaystyle a_\epsilon$ are real numbers, and $\displaystyle \epsilon$ is a basis such that $\displaystyle 1 \, \epsilon = \epsilon \, 1 = \epsilon$ and $\epsilon \,\epsilon = 0$.

### 2-1\. Multiplication  
$\displaystyle \hat{a}\hat{b} = (a_0 + a_\epsilon\epsilon)(b_0 + b_\epsilon\epsilon) = a_0b_0 + (a_0b_\epsilon + b_0a_\epsilon)\epsilon$ (\[Kavan 2008\] / A Dual Quaternion Tutorial / A.1 Dual Numbers).  

### 2-2\. Conjugation  

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
