## Notation  
$a$ real number  
$\boldsymbol{q}$ quaternion  
$\hat{a}$ dual number  
$\hat{\boldsymbol{q}}$ dual quaternion  

## Dual Numbder    
A dual number can be written as $\hat{a} = a_0 + a_\varepsilon\varepsilon$ (\[Kavan 2008\] / A Dual Quaternion Tutorial / A.1 Dual Numbers), where $a_0$ and $a_\varepsilon$ are real numbers, and ε is a basis such that $1 \, \varepsilon = \varepsilon \, 1 = \varepsilon$ and $\varepsilon \, \varepsilon = 0$.

### Multiplication  
$\hat{a}\hat{b} = (a_0 + a_\varepsilon\varepsilon)(b_0 + b_\varepsilon\varepsilon) = a_0b_0 + (a_0b_\varepsilon + b_0a_\varepsilon)\varepsilon$ (\[Kavan 2008\] / A Dual Quaternion Tutorial / A.1 Dual Numbers).  

### Square Root  
If $a_0 \gt 0$, then $\sqrt{a_0 + a_\varepsilon\varepsilon} = \sqrt{a_0} + \frac{a_\varepsilon}{2\sqrt{a_0}}\varepsilon$ (\[Kavan 2008\] / A Dual Quaternion Tutorial / A.1 Dual Numbers / Lemma 8).  
Proof:  
We assume that there exists the dual number $b_0 + b_\varepsilon\varepsilon$ such that $a_0 + a_\varepsilon\varepsilon = (b_0 + b_\varepsilon\varepsilon)(b_0 + b_\varepsilon\varepsilon)$, namely, $\sqrt{a_0 + a_\varepsilon\varepsilon} = b_0 + b_\varepsilon\varepsilon$.  
Evidently, we have $b_0b_0 = a_0$ and $2b_0b_\varepsilon = a_\varepsilon$. And thus, if $a_0 \gt 0$, we have $b_0 = \sqrt{a_0}$ and $b_\varepsilon = \frac{a_\varepsilon}{2\sqrt{a_0}}$.  

## Dual Quaternion  

A dual quaternion can be considered as a quaternion whose elements are dual numbers $\hat{\boldsymbol{q}} = \hat{q_w} + \hat{q_x}\text{i} + \hat{q_y}\text{j} + \hat{q_z}\text{k}$ where $\varepsilon\text{i} = \text{i}\varepsilon = i$, $\varepsilon\text{j} = \text{j}\varepsilon = j$ and $\varepsilon\text{k} = \text{k}\varepsilon = k$. Actually, a dual quaternion can also be considered as a dual number whose elements are quaternions $\hat{\boldsymbol{q}} = \boldsymbol{q_0} + \boldsymbol{q_\varepsilon}\varepsilon$ (\[Kavan 2008\] / A Dual Quaternion Tutorial / A.2 Dual Quaternions).  

### Multiplication  
$\hat{\boldsymbol{p}}\hat{\boldsymbol{q}} = (\boldsymbol{p_0} + \boldsymbol{p_\varepsilon}\varepsilon)(\boldsymbol{q_0} + \boldsymbol{q_\varepsilon}\varepsilon) = \boldsymbol{p_0}\boldsymbol{q_0} + (\boldsymbol{p_0}\boldsymbol{q_\varepsilon} + \boldsymbol{p_\varepsilon}\boldsymbol{q_0})\varepsilon$ where $\boldsymbol{p_0}\boldsymbol{q_0}$, $\boldsymbol{p_0}\boldsymbol{q_\varepsilon}$ and $\boldsymbol{p_\varepsilon}\boldsymbol{q_0}$ follow the rule of the multiplication of two ordinary quaternions (\[Kavan 2008\] / A Dual Quaternion Tutorial / A.2 Dual Quaternions).  

### Conjugation

#### The First Type Conjugation - Quaternion Conjugation  
${\hat{\boldsymbol{q}}}^* = {(\boldsymbol{q_0} + \boldsymbol{q_\varepsilon}\varepsilon)}^* = {\boldsymbol{q_0}}^* + {{\boldsymbol{q_\varepsilon}}^*}\varepsilon$ (\[Kavan 2008\] / A Dual Quaternion Tutorial / A.2 Dual Quaternions).  

#### The Second Type Conjugation - Dual Number Conjugation  
$\overline{\hat{q}} = \overline{\boldsymbol{q_0} + \boldsymbol{q_\varepsilon}\varepsilon} = \boldsymbol{q_0} - \boldsymbol{q_\varepsilon}\varepsilon$ (\[Kavan 2008\] / A Dual Quaternion Tutorial / A.2 Dual Quaternions).  

#### Quaternion Conjugation and Dual Number Conjugation are Commutative  
$\overline{{\hat{\boldsymbol{q}}}^*} = {\overline{\hat{q}}}^*$ (\[Kavan 2008\] / A Dual Quaternion Tutorial / A.2 Dual Quaternions).  
Proof:  
$\overline{{\hat{\boldsymbol{q}}}^*} = \overline{{(\boldsymbol{q_0} + \boldsymbol{q_\varepsilon}\varepsilon)}^*} = \overline{ {\boldsymbol{q_0}}^* + {{\boldsymbol{q_\varepsilon}}^*}\varepsilon} = {\boldsymbol{q_0}}^* - {{\boldsymbol{q_\varepsilon}}^*}\varepsilon = {(\boldsymbol{q_0} - \boldsymbol{q_\varepsilon}\varepsilon)}^* = {(\overline{\boldsymbol{q_0} + \boldsymbol{q_\varepsilon}\varepsilon})}^* = {\overline{\hat{q}}}^*$

### Norm  
(\[Kavan 2008\] / A Dual Quaternion Tutorial / A.2 Dual Quaternions / Lemma 9).

### The correspondence between rigid transformations and unit dual quaternions  

\[Kavan 2008\] / A.2 Dual Quaternions / Lemma 12  

## Reference  
\[Kavan 2007\][Ladislav Kavan, Steven Collins, Jiri Zara, Carol O'Sullivan. "Skinning with Dual Quaternions." I3D 2007.](http://www.cs.utah.edu/~ladislav/kavan07skinning/kavan07skinning.html)  
\[Kavan 2008\] [Ladislav Kavan, Steven Collins, Jiri Zara, Carol O'Sullivan. "Geometric Skinning with Approximate Dual Quaternion Blending." SIGGRAPH 2008.](http://www.cs.utah.edu/~ladislav/kavan08geometric/kavan08geometric.html)  
\[NVIDIA 2008\] [NVIDIA. "Skinning with Dual Quaternions." NVIDIA Direct3D SDK 10.5 Code Samples.](https://developer.download.nvidia.com/SDK/10.5/direct3d/samples.html#QuaternionSkinning)  
\[Vince 2011\] [John Vince. "Quaternions for Computer Graphics." Springer 2011.](https://link.springer.com/book/10.1007/978-0-85729-760-0)  
