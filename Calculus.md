## License  
```  
Copyright (C) YuqiaoZhang

This program is free software: you can redistribute it and/or modify it under the terms of the GNU Lesser General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU Lesser General Public License for more details.

You should have received a copy of the GNU Lesser General Public License along with this program.  If not, see <https://www.gnu.org/licenses/>
```  
   
### 集合    

等价关系 等价类 商集 划分    

等价类要么相等要么不相交 //即不相等的等价类一定不相交   
证明： //参考： 定理3-10.1 定理3-10.2 离散数学 左孝凌  
反证法 //Proof by contradiction

假设 $a \isin [b]_\sim$ 、$a \isin [c]_\sim$ 且 $[b]_\sim \ne [c]_\sim$   
我们有 $a \sim b$ 、$a \sim c$ 由于$\sim$是等价关系 我们有$b \sim c$   

$\forall \, e \isin [b]_\sim$ 有$e \sim b$ 又因为$b \sim c$ 有$e \sim c$ 即$e \isin [c]_\sim$  
并且$\forall \, e \isin [c]_\sim$ 有$e \sim c$ 又因为$b \sim c$ 有$e \sim b$ 即$e \isin [b]_\sim$  
即$\forall \, e \, , \, e \isin [b]_\sim \Leftrightarrow e \isin [c]_\sim$ 即$[b]_\sim = [c]_\sim$ 但是，这与 $[b]_\sim \ne [c]_\sim$ 矛盾，命题得证 //事实上，可以证明：$b \sim c \Leftrightarrow [b]_\sim = [c]_\sim$    
     
---       
     
集合的基数/势 Cardinal Number   
//\[Rudin 1976\] / 2\.3 Definition      

等势 equivalent  
   
可数的 countable / enumerable /denumerable  //与 正整数集 等势   
   
有理数集Q 是 可数的   
证明：  
表示成n/m //n可数 m可数  
   
实数集R 不是 可数的   
证明:  
Cantor //\[Rudin 1976\] / 2\.14 Theorem    
   
---  


### 拓扑 Topology
//补集 Complement //完成 Complete       

幂集 Power Set   
$\displaystyle \wp(X)$ //X的所有子集    

//指标集 Index Set   

---

//\[Rudin 1976\]并没有引入拓扑空间，而是以直接定义的方式引入度量空间  

拓扑 Topology / 拓扑空间 Topological Space           
\[陈天权 2009\] / 定义 7\.1\.1       
\[Yeh 2014\] / \[IV\] Borel σ-algebras //σ(Sigma)       
   
(X,τ)是拓扑空间 ⇔ τ是X上的拓扑 ⇔ τ ⊂ ℘(X) 且 ∅ ∈ τ 且 X ∈ τ 且 τ对无限并封闭 且 τ对有限交封闭 //此处的无限并没有要求可数 //可数即和自然数集等势 参见 集合的势/基数           

//用于不强调τ的情形     
X是拓扑空间 ⇔ ∃τ, (X,τ)是拓扑空间 ⇔ ∃τ, τ是X上的拓扑               

开集 Open Set    
\[陈天权 2009\] / 定义 7\.1\.1       
\[Yeh 2014\] / \[IV\] Borel σ-algebras //σ(Sigma)                   
(X,τ)是拓扑空间 ⇒ ( U是开集 ⇔ U ∈ τ )        

//用于不强调τ的情形      
X是拓扑空间 ⇔ ( U是开集 ⇔ ∃τ, (X,τ)是拓扑空间 且 U ∈ τ )           

开集/闭集三的概念源于对R上的开区间/闭区间的抽象      
无限个开区间的交可能是闭区间 比如：$\displaystyle \bigcap_{n \isin \N} (1-\frac{1}{n}, 2+\frac{1}{n})$=\[1,2\] //根据定义即可证明 //可能用到反证法       

拓扑间的包含关系     
finer/smaller/weaker    
coarser/larger/stronger    
       
---    
        
平凡拓扑 Trivial Topology     
离散拓扑 Discrete Topology   
    
//显然，对于任意集合X：  
//{∅, X}是X上的拓扑 被称为平凡拓扑 //\[陈天权 2009\] / 例 7\.1\.2         
//$\wp(X)$是X上的拓扑 被称为离散拓扑 //\[陈天权 2009\] / 例 7\.1\.1     
        
---     
        
领域 Neighborhood        
\[陈天权 2009\] / 定义 7\.1\.3   
\[Rudin 1976\] / 2.18 Definition (a)  
X是拓扑空间 且 x ∈ X ⇒ ( V ⊂ X 且 ( ∃ U, U是开集 且  x ∈ U 且 U ⊂ V ) ⇔ V是x的领域 )  

开领域 Open Neighbourhood    
\[陈天权 2009\] / 定义 7\.1\.3     
X是拓扑空间 且 x ∈ X ⇒ ( U是x的领域 且 U是开集 ⇔ U是x的开领域 )  
   
内点 Interior Point  
\[陈天权 2009\] / 定义 7\.1\.3   
\[Rudin 1976\] / 2.18 Definition (e)   
X是拓扑空间 且 x ∈ X 且 E ⊂ X ⇒ ( ∃ U, U是x的领域 且 U ⊂ E ⇔ x是N的内点 )   

定理：开集-内点   
\[陈天权 2009\] / 命题 7\.1\.1   
\[Rudin 1976\] / 2.18 Definition (f)   
定理：τ是X上的拓扑 ⇒ ( E是开集(即 E ∈ τ) ⇔ ∀ x ∈ E, x是E的内点 ) //E是开集 当且仅当 E的任何点都是E的内点   
      
> 证明   
>    
> 必要性    
> 对任意x ∈ E  
> 由于E是开集 我们有 存在E E是x的领域(因为x ∈ E 且 E是开集) 且 E ⊂ E   
> 即x是E的内点  
> 
> 充分性  
> 对任意x ∈ E 存在x的开领域$\displaystyle U_x$ 满足 $\displaystyle U_x$ ⊂ E //根据领域的定义，只要存在领域就一定存在开领域       
> 因此 以上开领域的并集 $\displaystyle \bigcup_{x \isin E} U_x$ ⊂ E  
>
> 并且 对任意x ∈ E 一定有x ∈ 以上其中的某一个$\displaystyle U_x$   
> 因此 E ⊂ $\displaystyle \bigcup_{x \isin E} U_x$  
>     
> 综上 E = $\displaystyle \bigcup_{x \isin E} U_x$   
> 根据拓扑的定义 E ∈ τ 即E是开集           
   
---
通常拓扑 Usual Topology  

R上的开集    
//\[陈天权 2009\] / §2\.5 23    
//定义方式在一定程度上源于“开集-内点”       
$\displaystyle \mathcal{U}$是R上的开集 ⇔  ∀x ∈ $\displaystyle \mathcal{U}$, ∃ϵ > 0, { y : ∣y − x∣ < ϵ } ⊂ $\displaystyle \mathcal{U}$ 

R上的通常拓扑   
R上的通常拓扑 T = { $\displaystyle \mathcal{U}$ | $\displaystyle \mathcal{U}$是R上的开集 }               
//R上的通常拓扑：R的所有可以表示为开区间的并的集合(Set)组成的集族(Collection) //\[陈天权 2009\] / 例 7\.1\.3     
//注：Collection与Set同义，表示“集合的集合”时，用Collection    
    
欧几里得空间 Euclidean Space     

$\displaystyle R^n$上的开集     
//\[陈天权 2009\] / 例 7\.1\.5           
//定义方式在一定程度上源于“开集-内点”       
$\displaystyle \mathcal{U}$是$\displaystyle R^n$上的开集 ⇔ ∀$\displaystyle \overrightarrow{x}$ ∈ $\displaystyle \mathcal{U}$, ∃ϵ > 0, { $\displaystyle \overrightarrow{y}$ : | $\displaystyle \overrightarrow{y}$ − $\displaystyle \overrightarrow{x}$| < ϵ } ⊂ $\displaystyle \mathcal{U}$     
其中： |$\displaystyle \overrightarrow{y}$ − $\displaystyle \overrightarrow{x}$|为欧几里得空间中的长度 且 B($\displaystyle \overrightarrow{x}$, ϵ) = { $\displaystyle \overrightarrow{y}$ : | $\displaystyle \overrightarrow{y}$ − $\displaystyle \overrightarrow{x}$| < ϵ }是以$\displaystyle \overrightarrow{x}$为球心ϵ为半径的开球    
    
$\displaystyle R^n$上的通常拓扑      
//\[陈天权 2009\] / 例 7\.1\.5           
$\displaystyle R^n$上的通常拓扑 T = { $\displaystyle \mathcal{U}$ | $\displaystyle \mathcal{U}$是$\displaystyle R^n$上的开集 }             
    
//~~一致收敛拓扑(Topology of Uniform Convergence)~~      
    
---   
   
$\displaystyle R^2$上的内点    
[同济大学数学系 2014] / 第九章 多元函数微分法及其应用 / 第一节 多元函数的基本概念 / 一、平面点集 *n维空间 / 1. 平面点集    
内点：如果存在P的某个领域U(P)，使得U(P) ⊂ E，那么称P为E的内点  

$\displaystyle R^2$上的开集-内点    
\[同济大学数学系 2014\] / 第九章 多元函数微分法及其应用 / 第一节 多元函数的基本概念 / 一、平面点集 *n维空间 / 1. 平面点集     
开集：如果点集E的点都是E的内点，那么称E为开集        
       
---         
      
极点(Limit Point)/聚点(Cluster Point / Accumulation Point)     
\[陈天权 2009\] / 定义 7\.1\.6   
\[Rudin 1976\] / 2.18 Definition (b)   
X是拓扑空间 且 E ⊂ X ⇒ ( x是E的聚点 ⇔ x ∈ E 且 ∀ x的领域U, (U - {x}) ∩ E ≠ ∅ )      

孤立点(Isolated Point)   
\[陈天权 2009\] / 定义 7\.1\.6   
\[Rudin 1976\] / 2.18 Definition (c)   
X是拓扑空间 且 E ⊂ X ⇒ ( x是E的孤立点 ⇔ x ∈ E 且 x不是E的聚点（即 ∃ x的领域U, (U - {x}) ∩ E = ∅） )  
   
导集(Derived Set)    
\[陈天权 2009\] / 定义 7\.1\.6   
\[Rudin 1976\] / 2.26 Definition
X是拓扑空间 且 E ⊂ X ⇒ E的导集E' = { x : x是E的聚点 }  
      
---   

闭集 Closed Set    
\[陈天权 2009\] / 定义 7\.1\.4      
X是拓扑空间 ⇒ ( X - U 是开集 ⇔ U是闭集 )                 
     
并且 可以用 德摩根定律(De Morgan's laws) 证明：    
对X上的离散拓扑： ∅是闭集 X是闭集 //一个集合可能既是开集又是闭集     
闭集的有限次并仍是闭集      
闭集的有限或无限次交仍是闭集   


闭包 Closure   
\[陈天权 2009\] / 定义 7\.1\.5      
\[Rudin 1976\] / 2\.27 Theorem         
定义： X是拓扑空间 且 E ⊂ X ⇒ E的闭包 $\displaystyle \overline{E}$ = $\displaystyle \bigcap_{S是闭集 且 E ⊂ S} S$ //E的闭包是所有包含E的闭集的交集    

定理： X是拓扑空间 且 E ⊂ X ⇒ ( E是闭集 ⇔ E = $\displaystyle \overline{E}$ ) //E的闭包是包含E的“最小”闭集   

> 证明  
>   
> 必要性  
> 显然 E ⊂ $\displaystyle \overline{E}$ //因为E的闭包是所有包含E的闭集的交集   
> 由于E也是“包含E的闭集“，因此 我们有 所有“包含E的闭集”的交集——即E的闭包——包含于E //即$\displaystyle \overline{E}$ ⊂ E   
> 综上 我们有 E = $\displaystyle \overline{E}$
>
> 充分性  
> 根据拓扑和闭集的定义 所有“包含E的闭集”的交集——即E的闭包——是闭集 //即$\displaystyle \overline{E}$是闭集          
> 由于E = $\displaystyle \overline{E}$ 即E是闭集    
> 
   
---   
   
定理：闭包-聚点/孤立点      
\[陈天权 2009\] / 命题 7\.1\.2       
X是拓扑空间 且 E ⊂ X ⇒ ( x ∈ $\displaystyle \overline{E}$ ⇔ ∀x的领域U, U∩E≠∅ ) //即$\displaystyle \overline{E}$ = { x : ∀x的领域U, U∩E≠∅ }         
   
> 证明    
>   
> 下面证明 x ∉ $\displaystyle \overline{E}$ ⇒ ∃ x的领域U, U ∩ E = ∅  
> 
> 因为 x ∉ $\displaystyle \overline{E}$ 我们有 x ∈ X - $\displaystyle \overline{E}$  
> 因为 $\displaystyle \overline{E}$是闭集 我们有X - $\displaystyle \overline{E}$是开集 因此X - $\displaystyle \overline{E}$是x的领域  
> 并且 显然 ( X - $\displaystyle \overline{E}$ ) ∩ E = ∅ 命题得证   
> 
> 因此 逆否命题成立 ∀ x的领域U, U ∩ E ≠ ∅ ⇒ x ∈ $\displaystyle \overline{E}$  
> 
> 下面证明 ∃x的领域U, U∩E=∅ ⇒ x∉$\displaystyle \overline{E}$  
> 
> 由于 U是X的领域 因此 x∈U 即 x∉X-U   
>   
> 由于 U是X的领域 因此 U是开集 从而 ( X-U )是闭集  
> 并且 由于 U∩E=∅ 因此 E ⊂ ( X-U ) 从而 ( X-U )是包含E的闭集  
>   
> 由于 x ∉ X - U 因此 x不属于 所有“包含E的闭集”的交集——即E的闭包$\displaystyle \overline{E}$ 命题得证  
>   
> 因此 逆否命题成立 x ∈ $\displaystyle \overline{E}$ ⇒ ∀ x的领域U, U ∩ E ≠ ∅      
> 
> 综上 命题得证   
>  
        
定理：闭包-导集   
\[陈天权 2009\] / 定义 7\.1\.6   
\[Rudin 1976\] / 2\.26 Definition     
X是拓扑空间 且 E ⊂ X ⇒ ( $\displaystyle \overline{E}$ = E ∪ E' )           
    
> 证明     
> 
> 由于  
> $\displaystyle \overline{E}$ = { x : ∀ x的领域U, U ∩ E ≠ ∅ } //根据”定理：闭包-聚点/孤立点“    
> E = { x : {x} ∩ E ≠ ∅ } //显然  
> E' = { x : ∀ x的领域U, (U - {x}) ∩ E ≠ ∅ } //根据 聚点 和 导集 的定义  
>   
> 显然 命题成立    
>  

---   
   
$\displaystyle R^2$上的聚点      
\[同济大学数学系 2014\] / 第九章 多元函数微分法及其应用 / 第一节 多元函数的基本概念 / 一、平面点集 *n维空间 / 1. 平面点集               
点集E以及它的边界∂E上的一切点都是E的聚点     

$\displaystyle R^2$上的闭集    
\[同济大学数学系 2014\] / 第九章 多元函数微分法及其应用 / 第一节 多元函数的基本概念 / 一、平面点集 *n维空间 / 1. 平面点集    
闭集：如果点集E的边界∂E⊂E，那么称E为闭集   

---   
    
稠密集 Dense Set       
\[陈天权 2009\] / 定义 7\.1\.9   
定义： X是拓扑空间 且 A ⊂ S ⊂ X ⇒ ( A在S中稠密 ⇔ S ⊂ $\displaystyle \overline{A}$ )            
//特别地，当A在X中稠密时，$\displaystyle \overline{A}$ = X //显然，X ⊂ $\displaystyle \overline{A}$    
    
根据“定理：闭包-聚点/孤立点”，A在S中稠密 ⇔ ∀x∈S, ∀x的领域U, U ∩ A ≠ ∅ //S中的任一点可以被A中的点很好的逼近    
      
---        
    
有理数集Q在实数集R的通常拓扑中稠密 //涉及到实数的戴德金构造法          
\[陈天权 2009\] / 例 7\.1\.10     
     
---            
     
可分空间 Separable Space      
\[陈天权 2009\] / 定义 7\.1\.10  
定义：X是拓扑空间 ⇒ ( X是可分空间 ⇔ ∃ A ⊂ X, A是可数的 且 A在X中稠密 )        
          
根据“定理：闭包-聚点/孤立点”， X是可分空间 ⇔ //存在可数的序列  
         
实数集R的通常拓扑是可分的 //有理数集Q是可数的 且 有理数集Q在实数集R的通常拓扑中稠密          
\[陈天权 2009\] / 定义 7\.1\.10     

---       
内部 Interior      
\[陈天权 2009\] / 定义 7\.1\.7  
定义： τ是X上的拓扑 且 E ⊂ X ⇒ E的内部$\displaystyle E \degree$ = $\displaystyle \bigcup_{S是开集 且 S ⊂ E} S$ //E的内部是所有包含于E的开集的并集            

//根据内点（Interior Point）的定义，显然，在E的内部的点一定是E的内点。   
     
定理： τ是X上的拓扑 且 E ⊂ X ⇒ ( E是开集 ⇔ E = $\displaystyle E \degree$ ) //E的内部是包含于E的“最大”开集  

> 证明  
>   
> 必要性  
> 显然 $\displaystyle E \degree$ ⊂ E //因为E的内部是所有包含于E的开集的并集   
> 由于E也是“包含E的开集“，因此 我们有 所有“包含于E的开集”的并集——即E的内部——包含E //即E ⊂ $\displaystyle E \degree$   
> 综上 我们有 E = $\displaystyle E \degree$
>
> 充分性  
> 根据拓扑的定义 所有“包含于E的开集”的并集——即E的内部——是开集 //即$\displaystyle  E \degree$是开集          
> 由于E = $\displaystyle E \degree$ 即E是开集    
>    
        
---  
    
边界 Boundary  
\[陈天权 2009\] / 定义 7\.1\.8     
定义： τ是X上的拓扑 且 E ⊂ X ⇒ E的边界$\displaystyle \partial E$ = $\displaystyle \overline{E}$ − $\displaystyle E \degree$ //    
       
定理： τ是X上的拓扑 且 E ⊂ X ⇒ ( E是开集且E是闭集 ⇔ $\displaystyle \partial E$ = ∅ ) //        
    
> 证明     
>      
> E是开集 ⇔ E = $\displaystyle E \degree$ //根据上面已经证明的定理     
> E是闭集 ⇔ E = $\displaystyle \overline{E}$ //根据上面已经证明的定理       
>       
> 必要性    
> E是开集且E是闭集 ⇒ E = $\displaystyle E \degree$ 且 E = $\displaystyle \overline{E}$ ⇒ $\displaystyle \partial E$ = $\displaystyle \overline{E}$ − $\displaystyle E \degree$ = ∅       
>     
> 充分性   
> $\displaystyle \partial E$ = ∅ ⇒ $\displaystyle \overline{E}$ − $\displaystyle E \degree$ = ∅ ⇒ $\displaystyle E \degree$ = $\displaystyle \overline{E}$    
>                   
>   
     
//边界一定是闭集   
//证明  
    
###    
    
---       
    
连续函数（拓扑空间） Continuous function (Topological Space)   
\[陈天权 2009\] / 定义 7\.2\.1      
           
X是拓扑空间 且 Y是拓扑空间 且 x ∈ X ⇒ ( 映射f : X→Y在点x处连续 ⇔ ∀ V是Y中f(x)的领域, ∃ U是X中x的领域 且 f(U) ⊂ V ) //在点x处连续 //像f(U) //半开半闭区间不属于(R的通常拓扑上的)领域               
      
X是拓扑空间 且 Y是拓扑空间 且 x ∈ X ⇒ ( 映射f : X→Y在点x处连续 ⇔ ∀ V是Y中f(x)的领域,$\displaystyle \operatorname{f^{-1}}$(V)是X中x的领域 ) //等价形式 //逆像$\displaystyle \operatorname{f^{-1}}$(V)         
       
> 证明         
>       
> //包含x的领域的集合一定是x的领域 并且 $\displaystyle \operatorname{f^{-1}}$(V)是X的子集中可能满足对应的像包含于V的最大的集合      
>      
        
X是拓扑空间 且 Y是拓扑空间 且 A ⊂ X ⇒ ( 映射f : X→Y 在A上连续 ⇔ ∀ x ∈ A, 映射f : X→Y 在点x处连续 ) //在集合上连续       
      
X是拓扑空间 且 Y是拓扑空间 ⇒ ( 映射f : X→Y 是连续映射 ⇔ 映射f : X→Y 连续 ⇔ 映射f : X→Y 在X上连续 ) //在定义域上连续       
      
---    
     
\[陈天权 2009\] / 命题 7\.2\.1   
X是拓扑空间 且 Y是拓扑空间 ⇒ ( 映射f : X→Y 连续 ⇔ ∀ V是Y中的开集, $\displaystyle \operatorname{f^{-1}}$(V)是X中的开集 )    
   
> 证明        
>    
> 必要性   
>     
> 对任意V是Y中的开集 我们有   
>   
> 对任意x ∈ $\displaystyle \operatorname{f^{-1}}$(V)           
> 根据逆像的定义 我们有f(x) ⊂ V     
> 由于 V是开集 根据连续函数的定义 我们有 $\displaystyle \operatorname{f^{-1}}$(V)是X中x的领域        
>    
> 即 对任意x ∈ $\displaystyle \operatorname{f^{-1}}$(V) 存在U=$\displaystyle \operatorname{f^{-1}}$(V) U是X中x的领域 且 U ⊂ $\displaystyle \operatorname{f^{-1}}$(V)    
> 根据 开集-内点定理 $\displaystyle \operatorname{f^{-1}}$(V)是X中的开集    
>       
> 充分性          
>            
> 对任意x ∈ X  我们有 
>    
> 对任意N ⊂ Y  N是X中f(x)的领域 我们有         
> 根据领域的定义 我们有 存在G是X中的开集 满足 f(x) ⊂ G ⊂ N  
> 
> 根据命题中的条件 我们有 $\displaystyle \operatorname{f^{-1}}$(G)是X中的开集              
> 由于 f(x) ⊂ G 因此 x ∈ $\displaystyle \operatorname{f^{-1}}$(G) 即 $\displaystyle \operatorname{f^{-1}}$(G)是X中x的领域    
> 由于 G ⊂ N 因此 $\displaystyle \operatorname{f^{-1}}$(G) ⊂ $\displaystyle \operatorname{f^{-1}}$(N) 根据领域的定义 我们有 $\displaystyle \operatorname{f^{-1}}$(N)是X中x的领域    
> 
> 即 对任意N ⊂ Y  N是f(x)的领域 我们有 $\displaystyle \operatorname{f^{-1}}$(N)是X中x的领域                    
> 根据连续映射的定义 映射f :X→Y连续       
>       

\[陈天权 2009\] / 命题 7\.2\.2   
X是拓扑空间 且 Y是拓扑空间 ⇒ ( 映射f : X→Y 连续 ⇔ ∀ V是Y中的闭集, $\displaystyle \operatorname{f^{-1}}$(V)是X中的开集 )    

//可以用 德摩根定律(De Morgan's laws) 证明    
   
---   
   
复合映射 Composite  Mapping     
\[陈天权 2009\] / 命题 7\.2\.3     
X是拓扑空间 且 Y是拓扑空间 且 Z 是拓扑空间 ⇒ ( 映射f : X→Y 连续 且 映射g : Y→Z 连续 ⇒ 映射 f ∘ g : X→Z 连续 ) //复合映射f ∘ g : X→Z    

> 证明        
>  
> 对任意V是Z中的开集 我们有  
> 
> 由于 映射g : Y→Z 连续 根据连续映射的定义 我们有 $\displaystyle \operatorname{g^{-1}}$(V)是Y中的开集    
> 由于 映射f : X→Y 连续 根据连续映射的定义 我们有 $\displaystyle \operatorname{f^{-1}}$[$\displaystyle \operatorname{g^{-1}}$(V)]是X中的开集     
>    
> 根据复合映射的定义 我们有 $\displaystyle \operatorname{{(f \circ g)}^{-1}}$(V) = $\displaystyle \operatorname{f^{-1}}$[$\displaystyle \operatorname{g^{-1}}$(V)]     
> 
> 即 对任意V是Z中的开集 我们有 $\displaystyle \operatorname{{(f \circ g)}^{-1}}$(V) 是X中的开集    
> 根据连续函数的定义 映射f ∘ g : X→Z 连续    
>        

---    
     
同胚 Homeomorphism /Topological Isomorphism /Bicontinuous function           
\[陈天权 2009\] / 定义 7\.2\.2       
X是拓扑空间 且 Y是拓扑空间 ⇒ ( 映射f : X→Y 是同胚(Homeomorphism) ⇔ 映射f : X→Y 是双射(bijection)(即单射(one-to-one)且满射(onto))  且 映射f : X→Y 连续 且 逆映射$\displaystyle \operatorname{f^{-1}}$ : X→Y 连续(即f是开映射(open mapping)) )    
     
同胚的 Homeomorphic     
\[陈天权 2009\] / 定义 7\.2\.2       
X是拓扑空间 且 Y是拓扑空间 ⇒ ( X和Y是同胚的(Homeomorphic) ⇔ ∃ 映射f : X→Y 是同胚 )   

显然 拓扑空间之间的同胚是等价关系    

     
---   
   
#### 完备集 Perfect Set    
    
分离公理 Separation Axiom   
T -> Tychonoff 吉洪诺夫     

Hausdorff 豪斯多夫   
分离空间 Separated Space  
T2空间   
\[陈天权 2009\] / 定义 7\.5\.2    
τ是X上的拓扑 ⇒ ( X是豪斯多夫空间 ⇔ ∀x,y∈X,x≠y, ∃x的领域U,y的领域V, U∩V=∅ )     



\[Rudin 1976\] / 2.18 Definition (h)   

         
         
            
       
#### 紧集 Compact Set    
   
有限覆盖定理/海涅-博雷尔定理 Heine–Borel theorem   
\[陈天权 2009\] / §2.5 6    
闭区间[a,b]被开区间族G（$\displaystyle \bigcup_{\alpha \isin A} I_\alpha$）覆盖 ⇒ 可以从开区间族中**选择**某个有限子族H（$\displaystyle \bigcup_{\alpha \isin B} I_\alpha$ 且 B ⊂ A）覆盖闭区间[a,b]   
   
> 证明 //证明过程与 \[陈天权 2009\] / 定理4.2.2 有一定相似性     
>  
> 构造集合 K = { x∈\[a,b\] : 存在开区间族的某个有限子族可以覆盖闭区间\[a,x\] }   
>
> 由于 闭区间\[a,b\]被开区间族G覆盖 又因为a∈\[a,b\] 显然 存在某个开区间(m,n)∈G 满足a∈(m,n) //**注：如果G为闭区间族，那么 这样的(m,n)就不一定存在** //可以结合闭集的定义：无限个闭集的并集并不一定是闭集     
> 在a和n之间任取一实数y 则有 \[a,y\]⊂(m,n) 即 存在有限子族{(m,n)}可以覆盖闭区间\[a,y\]   
> 即 y∈K 从而 K非空            
>     
> 根据K的定义 显然K中的元素一定小于或等于b 因此b是K的一个上界       
> 
> 根据LUB公理 K有上确界 不妨设M=supK   
>      
> 下面证明 存在某个有限子族可以覆盖闭区间\[a,M\] 即M∈K      
>              
> 由于M是K的上确界 从而M是K的一个上界 对于上文中属于K的y 有y≤M 又因为a\<y 从而有a\<M   
> 由于M是K的上确界 且b是K的一个上界 因此M≤b //上确界是最小上界  
> 从而 a\<M≤b 即 M∈\[a,b\]     
> 由于 闭区间\[a,b\]被开区间族覆盖 且 M∈\[a,b\] 显然 存在某个开区间(p,q)∈G 满足M∈(p,q) //**注：如果\[a,b\)为半开区间，那么 当M=b时 就不一定有点M被开区间族覆盖**    
>              
> 因此 M−q\>0 不妨取某个小于M−q且大于0的ϵ   
> 由于 M是K的上确界 根据上确界的性质 存在η>M-ϵ 满足η∈K 即存在某个有限子族（不妨设为H）可以覆盖\[a,η\]   
>    
> 由于 ϵ\<M−q 因此 M−ϵ\>M−(M−q)=q 从而 η>q    
> 因此 存在有限子族H∪{(p,q)}可以覆盖\[a,M\] 即 M∈K   
>         
> 下面证明 M=b   
>     
> 反证法，假设M≠b 由于M<=b(在上文中已经证明) 必有M\<b        
>         
> 对于上文中满足M∈(p,q)的开区间(p,q) 在M和q之间任取一实数q1     
> 由于M∈\[a,b\](在上文中已经证明) 存在某个有限子族（不妨设为H1）可以覆盖\[a,M\]       
> 因此 存在有限子族H1∪{(p,q)}可以覆盖\[a,q1\] 即 q1∈K    
>           
> 但是 q1\>M 这与M是K的上界矛盾 命题得证           
>    
   
> Proof   
>   
> We construct a set K = { x∈\[a,b\] : there exists a finite subcover of \[a,x\] }.      
> 
> Since G is the open cover of \[a,b\] and a∈\[a,b\], it is evident that there exists an open interval (m,n)∈G such that a∈(m,n). //**Note: If G was the closed cover, then such (m,n) would not exist.** //可以结合闭集的定义：无限个闭集的并集并不一定是闭集           
> Let y be a real number such that a\<y\<n. We have that \[a,y\]⊂(m,n). This means that {(m,n)} is a finite subcover of \[a,y\]. 
> This means that y∈K. It follows that K is not the empty set.    
>     
> By the definition of K, it is evident that all elements in K are less or equal than b. This means that b is an upper bound of K.              
>     
> By the LUB Axiom, there exists a supremum of K. Let M=supK.  
> 
> Next we try to show that M∈K.   
>   
> Since M is the supremum of K, we have that M is an upper bound of K. By the above y such that y∈K, we have that y≤M. Since a\<y， we have that a\<M.     
> Since M is the supremum of K and b is an upper bound of K, we have that M≤b. //The supremum is the smallest upper bound.    
> Then we have that a\<M≤b. This means that M∈\[a,b\].         
> Since G is the open cover of \[a,b\] and M∈\[a,b\], it is evident that there exists an open interval (p,q)∈G such that M∈(p,q). //**Note: If \[a,b\) was a half-open interval, then M would not be covered by G when M equals b.**       
>      
> It follows that M−q\>0. Let ϵ be a real number such that 0\<ϵ\<M−q.      
> Since M is the supremum of K, by the property of the supremum, there exists a real number η>M-ϵ such that η∈K. This means that there exists a finite subcover of \[a,η\]. We call that finite subcover H.                   
>       
> Since ϵ\<M−q, it follows that M−ϵ\>M−(M−q)=q. Thus, we have that η>q.         
> It follows that H∪{(p,q)} is a finite subcover of \[a,M\]. This means that M∈K.     
>        
> Next we try to show that M=b.     
>      
> Proof by Contradiction     
> We suppose M≠b. Since M<=b which we have shown above, we have that M\<b.     
>     
> By the above open interval (p,q) such that M∈(p,q), let q1 be a real number such that M\<q1\<q.   
> Since M∈\[a,b\] which we have shown above, there exists a finite subcover of \[a,M\]. We call that finite subcover H1.   
> It follows that H1∪{(p,q)} is a finite subcover of \[a,q1\]. This means that q1∈K.  
> 
> However M\<q1. This contradicts the fact that M is an upper bound of K.   
>   
>                              

//紧 compat -> 有限 finite    

---  
覆盖 Cover 
//覆盖的定义并不依赖于拓扑   
//见构造外测度

开覆盖 Open Cover    
\[陈天权 2009\] / 定义 7\.6\.1       
\[Rudin 1976\] / 2\.31 Definition      
    
X是拓扑空间 且 Y ⊂ X 且 C = {$\displaystyle U_\alpha$ | α ∈ A }  ⇒ (  C是Y的覆盖 ⇔ C是E的覆盖 且 ∀"α ∈ A","$\displaystyle U_\alpha$是X上的开集" )    

子覆盖 Subcover   
\[陈天权 2009\] / 定义 7\.6\.1       
\[Rudin 1976\] / 2\.31 Definition  

τ是X上的拓扑 且 E⊂X 且 $\displaystyle \bigcup_{\alpha \isin A} G_\alpha$是E的开覆盖 ⇒ ( $\displaystyle \bigcup_{\alpha \isin B} G_\alpha$是$\displaystyle \bigcup_{\alpha \isin A} G_\alpha$（关于E）的子覆盖 ⇔ B ⊂ A 且 E ⊂ $\displaystyle \bigcup_{\alpha \isin B} G_\alpha$ )   

有限子覆盖 Finite Subcover     
\[陈天权 2009\] / 定义 7\.6\.1       
\[Rudin 1976\] / 2\.31 Definition   
          
τ是X上的拓扑 且 E⊂X 且 $\displaystyle \bigcup_{\alpha \isin A} G_\alpha$是E的开覆盖 ⇒ ( $\displaystyle \bigcup_{\alpha \isin B} G_\alpha$是$\displaystyle \bigcup_{\alpha \isin A} G_\alpha$（关于E）的子覆盖 ⇔ B是有限集 且 $\displaystyle \bigcup_{\alpha \isin B} G_\alpha$是$\displaystyle \bigcup_{\alpha \isin A} G_\alpha$（关于E）的子覆盖 )    
       
紧集 Compact Set   
\[陈天权 2009\] / 定义 7\.6\.1       
\[Rudin 1976\] / 2\.31 Definition    
      
τ是X上的拓扑 且 K⊂X ⇒ ( K是紧集 ⇔ ∀G,G是K的开覆盖 ∃H,H是G（关于K）的有限子覆盖 ) //从（有限或无限）开覆盖G中**选择**有限个开集（H的元素）来覆盖K     
         
R上的闭区间是（关于R的通常拓扑的）紧集   
\[陈天权 2009\] / 例 7\.6\.1       

根据 有限覆盖定理 即可证明

豪斯多夫空间-紧集-闭集        
\[陈天权 2009\] / 命题 7\.6\.4       
X是豪斯多夫空间 且 K⊂X ⇒ ( K是紧集 ⇒ K是闭集 ) //紧集必闭          

> 证明        
>                    
> 下面证明 ∀x∉E ⇒ x∉$\displaystyle \overline{E}$    
>
> 对任意给定的x∉E，我们有：  
>            
> 对于任意y∈E，我们有：    
> 因为x∉E 从而x≠y    
> 由于X是豪斯多夫空间 存在x的领域$\displaystyle U_x$和y的领域$\displaystyle V_y$ 满足$\displaystyle U_x$∩$\displaystyle V_y$=∅       
>                 
> 显然 E中的任意一点 一定属于 以上的某一个y的领域 即 E⊂$\displaystyle \bigcup_{y \isin K} V_y$        
> 从而 $\displaystyle \bigcup_{y \isin K} V_y$是E的一个开覆盖  
> 由于 E是紧集 存在E的有限子覆盖$\displaystyle \bigcup_{y \isin F} V_y$ //F是有限集 //即从K中选择有限个点组成的集合F       
>         
> 从而 与以上y的领域对应的x的领域（即满足$\displaystyle U_x$∩$\displaystyle V_y$=∅的x的领域）的交集$\displaystyle \bigcap_{y \isin F} {U_x}_y$是开集 //根据拓扑的定义 **有限个**开集的交集才一定是开集 因此我们必须先证明F是有限集            
>         
> 显然 x∈$\displaystyle \bigcap_{y \isin F} {U_x}_y$ //因为x属于任意x的领域  
>     
> 又因为 E ∩ $\displaystyle \bigcap_{y \isin F} {U_x}_y$ ⊂ $\displaystyle \bigcup_{y \isin K} V_y$ ∩ $\displaystyle \bigcap_{y \isin F} {U_x}_y$ = $\displaystyle \bigcup_{y \isin K} (V_y \cap \bigcap_{y \isin F} {U_x}_y)$ ⊂ $\displaystyle \bigcup_{y \isin K} (V_y \cap U_x )$ = ∅     
> 
> 根据定理“$\displaystyle \overline{E}$ = { x : ∀x的领域U, U∩E≠∅ }”，我们有x∉$\displaystyle \overline{E}$    
>    
> 从而 以上命题的逆否命题成立：∀x∈$\displaystyle \overline{E}$ ⇒ x∈E 即 $\displaystyle \overline{E}$ ⊂ E          
>               
> 又因为 E ⊂ $\displaystyle \overline{E}$ //根据闭包的定义，显然      
> 我们有 E = $\displaystyle \overline{E}$         
>       
> 根据定理“E是闭集 ⇔ E = $\displaystyle \overline{E}$“，E是闭集    
>          
>                                                                    
          
        
---                
          
斯通-魏尔施特拉斯逼近定理 / Stone-Weierstrass Theorem      
//\[陈天权 2009\] / 定理 7\.7\.2         
//\[Rudin 1976\] / 7\.32 Theorem       
         
                
### 度量 Metric      
      
度量空间 Metric Space   
                      
距离函数 Distance Function 
度量 Metric      
不可分的同一性 Identity of Indiscernibles  
对称性 Symmetric   
次可加性 Subadditivity  
三角不等式 Triangle Inequality  
//\[陈天权 2009\] / 定义 7\.3\.1       
//\[Rudin 1976\] / 2.15 Definition   
(M,d)是度量空间 ⇔ d是M上的距离函数/度量 ⇔ d是M×M到R的映射 且 满足 不可分的同一性 d(x,y) = 0 ⇔ x = y 、 对称性 d(x,y) = d(y,x) 和 次可加性/三角不等式 d(x,z) ≤ d(x,y) + d(y,z)    
   
诱导 Induce   
   
度量空间 诱导 拓扑空间 //拓扑空间是度量空间的弱化 没有距离的概念 只有领域的概念  
//\[陈天权 2009\] / 命题 7\.3\.1   
//\[陈天权 2009\] / 定义 7\.3\.3   
度量空间 可诱导得到 对应的拓扑空间   
拓扑空间的开集 被定义为 由度量定义的开球                
                  
                       
欧几里得空间 Euclidean Space     
$\displaystyle R^k$上的欧几里得空间 度量 d(x,y) = |x - y| //度量被定义为向量的模   
         
                     

### 实数完备性 Completeness of the real numbers //实数系连续性  

最大数 max  
最小数 min    
有上界 （be） bounded above  
有下界 （be） bounded belowed    
上界 upper bound  
下界 lower bound  
上确界 supremum //最小上界 least upper bound //最小：任何比它小的实数值都不是上界        
下确界 infimum //最大下界 greatest lower bound    
  
定理： 设M = supE，则 $\forall  \, \epsilon > 0, \, \exists \, x \isin E, \, x > M - \epsilon$    
Proof by Contradiction  
suppose $\exists \, x \isin E, \, x > M - \epsilon$ is not true  
then $\forall \, x \isin E, \, x <= M - \epsilon$, which implies $M - \epsilon$ is an upper bound of E  
since $\epsilon > 0$, $M - \epsilon$ is less than M, which contradicts the given statement "M is the least upper bound"  
   
定理： 设M = infE，则 $\forall  \, \epsilon < 0, \, \exists \, x \isin E, \, x < M + \epsilon$  
证明从略   
   
---   
    
最小上界性（Least Upper Bound Property）如果非空的实数子集有上界，那么它一定有上确界 //戴德金完备性（Dedekind Completeness）     
LUB公理（LUB Axiom) //直接看作公理 //\[Rudin 1976\] 1.10 Definition    
    
最大下界性（Greatest Lower Bound Property）    
> 证明 //\[Rudin 1976\] 1.11 Theorem    
>    
> 不妨设 非空的实数子集为B 设 L = { y : y是B的一个下界 }   
> 由于B非空 任取B中的某个x 容易证明 有 x是L的一个上界 根据最小上界性 L有上确界 不妨设为α    
>   
> 容易证明 **对B中的任意x 都有 x是L的一个上界** //证明的关键   
由于α是L的上确界 根据上确界定义 对任意y<α 都有 y不是L的一个上界 //根据逆否命题等价性 对任意L的上界x 都有x>=α  
因此 对B中的任意x 都有 都有x>=α 即α是B的一个下界 **可以理解成：上确界是最小上界 既然B中的元素都是L的上界，那么B中的元素都大于上确界α**  
> 
> 又因为α是L的一个上界  
对任意β>α 都有 β不属于L 即β不是B的下界   
>
> 综上 α是B的一个下界 且 对任意β>α 都有 β不是B的下界 命题得证  

单调收敛定理（Monotone Convergence Theorem） 单调有界数列必有极限 //单调收敛原理    
   
单调递增 monotonically increasing  
单调递减 monotonically decreasing  
   
>证明 单调递增情形  
由于{xn}有界 根据LUB公理 {xn}有上确界，不妨设c=sup{xn}  
根据上确界性质 对任意ϵ>0 存在a属于{xn} 满足a>c-ϵ 不妨设a的下标为A 即a=xA   
由于{xn}单调递增 取N=A 对任意n>N 满足xn>xN=xA>c-ϵ 即xn-c>-ϵ  
又由于上界的定义 任意xn\<c 即xn-c \< 0 由于ϵ>0 有xn-c<ϵ  
综上|xn-c|<ϵ 命题得证   
>
> 单调递减情形   
根据之前的证明{-xn}有极限  
不妨设{-xn}极限为A 根据极限的定义不难证明 {xn}的极限为-A  
   

柯西收敛准则（Cauchy's Convergence Test） //柯西极限存在准则/柯西审敛原理 //柯西完备性（Cauchy Completeness）    
数列{xn}有极限的充分必要条件：$\exists \, A \isin \R , \, \lim\limits_{n \rightarrow \infin}x_n = A \ \Leftrightarrow \forall \, \epsilon > 0 , \, \exists \, N \isin \N^+ , \, \forall \, m > N , \, n > N , \, |x_m - x_n| < \epsilon$   
//\[Bartle 2011\] / 3.5.5 Cauchy Convergence Criterion  
//\[陈天权 2009\] / 定理 3.2.3  
>证明  
>  
> 必要性 //Necessary    
let lim Xn = a  
for all given ϵ > 0  
by the definition of the limit of a sequence, there exists a K(ϵ/2) ∈ N such that for all n > K(ϵ/2) ∈ N, we have |xn - a| < ϵ/2    
let H(ϵ) = K(ϵ/2)   
for all n,m > H(ϵ),  we have |xn - xm| = |(xm - a) - (xn -a)| <= | xm - a | + | xn -a | = ϵ/2 + ϵ/2 = ϵ //triangle inequality  //绝对值不等式  
>
> 充分性 //Sufficiency  
> we construct two sequence ix_k = inf{ xn | n > k } and sx_k = sup{ xn | n > k }  
> 
> first we try to prove that the limit of ix_k and sx_k exists  
> 
> let ϵ = 1, there exists a H(1) ∈ N such that for all n,m > H(ϵ)， it holds that |xn - xm| < 1  
in other words, xm - 1 < xn < xm + 1
>  
> let m = H(1)， we have that for all n > H(1) it holds that xH(1) - 1 < xn < xH(1) + 1
> 
> let M = max { |x1|, |x2| ... |xH(1)|, |xH(1) - 1|, |xH(1) + 1| }, we have that for all xn, it holds that |xn| < M  
> by the definition of bounded above/below, xn is bounded   
>
> by the definition of the supremum and infimum, sx_k is monotonically decreasing and ix_k is  monotonically increasing  
>
> by the Monotone Convergence Theorem, the limit of ix_k and sx_K exists  
> let lim ix_k = α and lim sx_k = β  
>
> second we try to prove that lim (sx_k - ix_k) = 0  
> for all given ϵ > 0  
>
> there exists a H(ϵ/2) ∈ N such that for all n,m > H(ϵ)， it holds that |xn - xm| < ϵ   
in other words, xm - ϵ < xn < xm + ϵ
> 
> let m = H(ϵ)， we have that for all n > H(ϵ) it holds that xH(ϵ) - ϵ < xn < xH(ϵ) + ϵ  
>
> by the definition of the upper/lower bound, xH(ϵ) - ϵ is an lower bound of { xn | n > H(ϵ) } and xH(ϵ) + ϵ is an upper bound of { xn | n > H(ϵ) }  
>
> by the definition of the supremum(least upper bound) and infimum(greatest lower bound), we have that xH(ϵ) - ϵ <= inf{ xn | n > H(ϵ) } <= { xn | n > H(ϵ) } <= xH(ϵ) + ϵ  
it follows that 0 <= sup{{ xn | n > H(ϵ) } - inf{ xn | n > H(ϵ) } <= xH(ϵ) + ϵ - (xH(ϵ) - ϵ) = 2ϵ 
> 
> we have shown that for all given ϵ > 0 there exists a H(ϵ/2) ∈ N such that | (sx_k - ix_k) - 0 | < 2ϵ  
>
> in other words, for all given η > 0, let e = η/2, we have that there exists a H(ϵ/2) ∈ N such that | (sx_k - ix_k) - 0 | < 2ϵ = 2*(η/2) = η  
> 
> by the definition of the limit of the sequence, lim (sx_k - ix_k) = 0 
>
> third we try to prove the conclusion  
> by 极限的四则运算, lim (sx_k - ix_k) = lim sx_k - lim ix_k = α - β  
since lim (sx_k - ix_k) = 0, we have that α - β = 0 in other words α = β  
>  
> by the construction of ix_k and sx_k, we have that ix_k <= xn <= sx_k  
by the Squeeze Thereom, we have that the limit of xn exists and lim xn = α = β  

### 数列（sequence）  

数列极限定义   
$\forall \, \epsilon > 0 , \, \exists \, K(\epsilon) \isin \N , \, \forall \, n > K(\epsilon) , \, |x_n - a| < \epsilon \Leftrightarrow \lim\limits_{n \rightarrow \infin}x_n = a$   
N(ϵ)用于强调N的选择依赖于ϵ //[Bartle 2011] \\ 3\.1\.3 Definition  

证明极限  
对每个ϵ，求出相应的N //严格地来讲，只需证明N存在，并不需要给出N的具体值，但大多数情况下都能较便利地求出   
  
证明极限不存在  
给出反例ϵ 证明相应的N不存在（根据之前的总结，证明不存在往往可以用反证法） //严格地来讲，只需证明反例ϵ存在，并不需要给出ϵ的具体值，但大多数情况下都能较便利地求出  

### 级数（series）  

部分和 partial sum  
收敛 convergent  
发散 divergent  
(一般)项 term   



数列{xn}的部分和数列{sn} 即数列{xn}生成的级数  
xn称为级数的一般项  
数列{sn}的极限称为级数的和（sum）或值（value） //通常记作${\displaystyle\sum_{n=1}^\infin} x_n$   

调和级数（Harmonic Series）  
${\displaystyle\sum_{n=1}^\infin} \frac{1}{n} = 1 + \frac{1}{2} + \frac{1}{3} + ... + \frac{1}{n} + ...$   

几何级数（Geometric Series） //等比数列部分和  
${\displaystyle\sum_{n=0}^\infin} r^n = 1 + r + r^2 + ... + r^n + ...$   

#### 级数收敛的必要条件  
The nth Term Test //\[Bartle 2011\] \\ 3\.7\.3 The nth Term Test  
级数收敛的必要条件 //\[同济大学数学系 2014\] 第十二章 无穷级数 / 第一节 常数项级数的概念和性质 / 二 收敛级数的基本性质 性质5  

//一般使用逆否命题 用于证明级数发散  
  
级数 $\displaystyle{\sum_{n = 1}^\infin} x_n$ ⇒ 收敛 $\lim\limits_{n \rightarrow \infin}x_n = 0$  
>Proof //证明  
let $\displaystyle{\sum_{n = 1}^\infin} x_n = a$ and $s_n = \displaystyle{\sum_{k = 1}^n} x_k$   
then $\lim\limits_{n \rightarrow \infin} x_n = \lim\limits_{n \rightarrow \infin} (s_n - s_{n-1}) = \lim\limits_{n \rightarrow \infin} s_n - \lim\limits_{n \rightarrow \infin} s_{n-1} = a - a = 0$ //数列极限的运算法则  
  
#### 柯西审敛原理  
Cauchy's convergence test //Wikipedia  
Cauchy Criterion for Series //\[Bartle 2011\] \\ 3\.7\.4 Cauchy Criterion for Series  
柯西审敛原理 //\[同济大学数学系 2014\] 第十二章 无穷级数 / 第一节 常数项级数的概念和性质 / 三 柯西审敛原理  
级数 $\displaystyle{\sum_{n = 1}^\infin} x_n$ 收敛 ⇔ $\forall \, \epsilon > 0, \, \exists \, H(\epsilon) \isin \N, \, \forall \, m > n \ge H(\epsilon), \, |\displaystyle{\sum_{k = n}^m} x_n| < \epsilon$    
//由于级数本身也是一种数列 将 对数列的柯西审敛原理 应用至此即可   

#### 正项级数及其审敛法 //非负项级数    
正项级数 //let xn be a sequence of nonnegative real numbers //零或正数  

##### 正项级数收敛 ⇔ 部分和数列有界 
//\[Bartle 2011\] / 3\.7\.5 Theorem  
//\[同济大学数学系 2014\] 第十二章 无穷级数 / 第二节 常数项级数的审敛法 / 一 正项级数及其审敛法 定理1  
//\[陈天权 2009\] 定理 3.3.1  
>证明  
显然 正项级数的部分和数列单调递增  
根据 单调收敛定理 命题即得证   

调和级数（Harmonic Series） $\displaystyle{\sum_{n = 1}^\infin} \frac{1}{n}$ 发散    
> Proof //证明  
>    
> 下面证明 $\displaystyle{\sum_{n = 1}^{2^n}} \frac{1}{n}$ 无界 //\[Bartle 2011\] / 3\.3\.3 Examples(b)   
>    
> $\displaystyle{\sum_{k=1}^{2^n}} \frac{1}{k}$ = $1 +\frac{1}{2} + (\frac{1}{3} + \frac{1}{4}) + ... + (\frac{1}{2^{n-1}+1} + ... + \frac{1}{2^n})$  
\> $1 +\frac{1}{2} + (\frac{1}{4} + \frac{1}{4}) + ... + (\frac{1}{2^{n}} + ... + \frac{1}{2^n})$  
= $1 + \frac{1}{2} + ... + \frac{1}{2}$  
= $1 + \frac{k}{2}$  
>   
> 我们有 $\forall \, M > 0, \, \exists \, H(M) = 2^{2M} \isin \N , \, \forall \, n > H, \, |\displaystyle{\sum_{k=1}^{n}} \frac{1}{k}| >= |\displaystyle{\sum_{k=1}^{2^{2M}}} \frac{1}{k}| > 1 + \frac{2M}{2} > M$ 因此 $\displaystyle{\sum_{n=1}^{2^n}} \frac{1}{n}$ 无界  
>   
> 根据 正项级数及其审敛法 我们有 $\displaystyle{\sum_{n = 1}^{2^n}} \frac{1}{n}$ 发散   
  
p-series $\displaystyle{\sum_{n = 1}^\infin} \frac{1}{n^p}$ 当p>1时 收敛   
> 证明   
>   
> 下面证明有界 //\[Bartle 2011\] / 3\.7\.6 Examples(d)   
>  
> $\displaystyle{\sum_{k = 1}^{2^n -1}} \frac{1}{k^p}$ = $1 + (\frac{1}{2^p} + \frac{1}{3^p}) + ... + + (\frac{1}{{(2^{n-1})}^p} + ... + \frac{1}{{(2^n)}^p})$   
\< $1 + (\frac{1}{2^p} + \frac{1}{2^p}) + ... + + (\frac{1}{{(2^{n-1})}^p} + ... + \frac{1}{{(2^{n-1})}^p})$   
= $1 + \frac{1}{2^{p-1}} + ... + {(\frac{1}{2^{p-1}})}^{n-1}$ //p>1 $\frac{1}{2^{p-1}} \ne 1$     
= $\frac{1 - {(\frac{1}{2^{p-1}})}^n}{1 - \frac{1}{2^{p-1}}}$ < $\frac{1}{1 - \frac{1}{2^{p-1}}}$ 
>   
> 取M=$\frac{1}{1 - \frac{1}{2^{p-1}}}$ 即证明有界    

欧拉数（Euler's number）  
级数 $\displaystyle{\sum_{n=0}^\infin} \frac{1}{n!}$ 收敛   
> 证明 //\[Rudin 1976\] / 3.30 Definition       
>   
> $\displaystyle{\sum_{n=0}^\infin} \frac{1}{n!} = 1 + 1 + \frac{1}{1 \cdot 2} + \frac{1}{1 \cdot 2 \cdot 3} + ... + \frac{1}{1 \cdot 2 \cdot ... \cdot n}$    
> < $1 + 1 + \frac{1}{2} + \frac{1}{2^2} + ... + \frac{1}{2^{n-1}}$      
> = $1 + 1 + (1 - \frac{1}{2^{n-1}})$  
> = $3 - \frac{1}{2^{n-1}}$  
> < 3  
  
欧拉数定义：$\displaystyle e = \sum_{n=0}^\infin \frac{1}{n!}$  
  
---  
  
$\lim\limits_{n \rightarrow  \infin} {(1+\frac{1}{n})}^n = e$  
> 证明   
> 
> ${(1+\frac{1}{n})}^n$  
> //二项式定理 //Binormial Theorem    
> = $C_n^0 \cdot 1^n + C_n^1 \cdot 1^{n-1} \cdot {(\frac{1}{n})}^1 + C_n^2 \cdot 1^{n-2} \cdot {(\frac{1}{n})}^2 + C_n^3 \cdot 1^{n-3} \cdot {(\frac{1}{n})}^3 + ... + C_n^n \cdot {(\frac{1}{n})}^n$ //二项式定理   
> = $1 + \frac{n}{n} + \frac{1}{2!} \cdot \frac{(n) \cdot (n-1)}{n^2} + \frac{1}{3!} \cdot \frac{(n) \cdot (n-1) \cdot (n-2)}{n^3} + ... + \frac{1}{n!} \cdot \frac{(n) \cdot (n-1) \cdot (n-(n-1))}{n^n}$  
> = $1 + 1 + \frac{1}{2!} \cdot (1 - \frac{1}{n}) + \frac{1}{3!} \cdot (1 - \frac{1}{n}) \cdot (1 - \frac{2}{n}) + ... + \frac{1}{n!} \cdot (1 - \frac{1}{n}) \cdot (1 - \frac{2}{n}) \cdot ... \cdot (1 - \frac{n-1}{n})$  
> ≤ $1 + 1 + \frac{1}{2!} + \frac{1}{3!} + ... + \frac{1}{n!}$  
> = ${\displaystyle\sum_{n=0}^\infin} \frac{1}{n!}$  
> 
> 尝试用 Squeeze Theorem   
> 注：${(1+\frac{1}{n})}^n$是单调递增的 //尝试根据单调递增找出下限   

##### 比较审敛法/Comparison Test  

正项级数${\displaystyle\sum_{n=0}^\infin} a_n$和${\displaystyle\sum_{n=0}^\infin} b_n$满足$a_n$ >= $b_n$ ⇒ ${\displaystyle\sum_{n=0}^\infin} a_n$收敛，则${\displaystyle\sum_{n=0}^\infin} b_n$一定收敛（即逆否命题：${\displaystyle\sum_{n=0}^\infin} b_n$发散，则${\displaystyle\sum_{n=0}^\infin} a_n$一定发散）  
//\[Bartle 2011\] / 3\.7\.7 Comparison Test  
//\[Rudin 1976\] / 3\.25 Theorem   
//\[同济大学数学系 2014\] 第十二章 无穷级数 / 第二节 常数项级数的审敛法 / 一 正项级数及其审敛法 定理2（比较审敛法）  
//\[陈天权 2009\] 定理 3\.3\.3  

> 证明  
>  
> ${\displaystyle\sum_{n=0}^\infin} a_n$收敛 则${\displaystyle\sum_{n=0}^\infin} a_n$有界  
> 由于$a_n$ >= $b_n$ 因此${\displaystyle\sum_{n=0}^\infin} b_n$一定有界   
> 根据“正项级数收敛 ⇔ 部分和数列有界” 则${\displaystyle\sum_{n=0}^\infin} b_n$一定收敛   

#### 交错级数及其审敛法  

交错调和级数 （Alternating Harmonic Series） $\displaystyle{\sum_{n = 1}^\infin} \frac{{(-1)}^{n+1}}{n}$ 收敛  
> 证明  
> 
> $|\displaystyle{\sum_{k = n}^m} \frac{{(-1)}^{k+1}}{k}|$   
> = $\frac{1}{n} - (\frac{1}{n+1} - \frac{1}{n+2}) - ... - \frac{1}{n+(m-n)+1}$  
> < $\frac{1}{n}$    
>
> 对任意给定的ϵ>0 取H(ϵ)为任意某个大于$\frac{1}{\epsilon}$的整数 对于任意m>n≥H(ϵ) $|\displaystyle{\sum_{k = n}^m} \frac{{(-1)}^{k+1}}{k}|$ < $\frac{1}{n}$ < $\frac{1}{\frac{1}{\epsilon}}$ = ϵ   
> 根据柯西收敛准则 级数 $\displaystyle{\sum_{n = 1}^\infin} \frac{{(-1)}^{n+1}}{n}$ 收敛

#### 绝对收敛（Absolute Convergence）与条件收敛（Conditionally Convergent / Nonabsolutely Convergent）  
级数 $\displaystyle{\sum_{n = 1}^\infin} |x_n|$ 收敛 ⇒ 级数 $\displaystyle{\sum_{n = 1}^\infin} x_n$ 收敛  
> 证明  
> 
> 根据柯西收敛准则  由于 级数 $\displaystyle{\sum_{n = 1}^\infin} |x_n|$ 收敛 我们有 $\forall \, \epsilon > 0, \, \exists \, H(\epsilon) \isin \N, \, \forall \, m > n \ge H(\epsilon), \, | \displaystyle{\sum_{k = n}^m} |x_k| | < \epsilon$     
>
> 根据三角不等式 $| \displaystyle{\sum_{k = n}^m} x_k | \le \displaystyle{\sum_{k = n}^m} |x_k| = | \displaystyle{\sum_{k = n}^m} |x_k| | < \epsilon$  
>
> 因此 我们有  $\forall \, \epsilon > 0, \, \exists \, H(\epsilon) \isin \N, \, \forall \, m > n \ge H(\epsilon), \, | \displaystyle{\sum_{k = n}^m} x_k | < \epsilon$ 根据柯西收敛准则 级数 $\displaystyle{\sum_{n = 1}^\infin} x_n$ 收敛   

绝对收敛（Absolute Convergence） 一定 收敛  
只收敛 但不绝对收敛 称为 条件收敛 //举例 交错调和级数收敛 但调和级数分散 因此调和级数绝对收敛  

### 函数项级数（Series of Functions）  

#### 函数项数列（Sequences of Functions）  
//函数项数列fn(x)在A上逐点（Pointwise）收敛 //$\operatorname{f_n}(x) \rightarrow \operatorname{f}(x)$ on A   
$\forall \, x \isin A , \, \lim\limits_{n \rightarrow \infin} \operatorname{f_n}(x) = \operatorname{f}(x)$ //对给定x，fn(x)即常数项数列   
$\forall \, \epsilon > 0 , \, x \isin A , \, \exists \, K(\epsilon , \, x) \isin \N , \, \forall \, n > K(\epsilon , \, x) , \, |\operatorname{f_n}(x) - \operatorname{f}(x)| < \epsilon$ ⇔ $\operatorname{f_n}(x) \rightarrow \operatorname{f}(x)$ on A  
  
//函数项数列fn(x)在A上一致（Uniform）收敛 //$\operatorname{f_n}(x) \rightrightarrows \operatorname{f}(x)$ on A    
$\forall \, \epsilon > 0 , \, \exists \, K(\epsilon) \isin \N , \, \forall \, n > K(\epsilon)  , \, x \isin A , \, |\operatorname{f_n}(x) - \operatorname{f}(x)| < \epsilon$ ⇔ $\operatorname{f_n}(x) \rightrightarrows \operatorname{f}(x)$ on A  

#### 函数项级数（Series of Functions）  
\[Bartle 2011\] 基于 函数项数列的逐点收敛 定义 函数项级数  


#### 幂级数（Power Series）  
${\displaystyle\sum_{n = 0}^{\infin}} a_nx^n$ = $a_0 + a_1x + ... + + a_nx^n + ...$ //因为$0^0$没有定义，是否应当写为$\displaystyle 1 + \sum_{n = 1}^{\infin} a_nx^n$？          

 Cauchy-Hadamard Theorem  
//\[Bartle 2011\] / 9\.4\.9 Cauchy-Hadamard Theorem  
//\[Rudin 1976\] / 3\.39 Theorem  
//\[同济大学数学系 2014\] / 第十二章 无穷级数 / 第三节 幂级数 / 二 幂级数及其收敛性 / 定理2    
//\[陈天权 2009\] / 定理 3\.5\.1   
  
极限$\lim\limits_{n \rightarrow \infin} \sqrt[n]{| a_n |}$存在 ⇒ 设R = $\frac{1}{\lim\limits_{n \rightarrow \infin} \sqrt[n]{| a_n |}}$，我们有：当|x| \< R时，幂级数${\displaystyle\sum_{n = 0}^{\infin}} a_nx^n$收敛；当|x| \> R时，幂级数${\displaystyle\sum_{n = 0}^{\infin}} a_nx^n$发散。   
//R又被称作 收敛半径（radius of convergence）    

> 证明  
>    
> 由于$\lim\limits_{n \rightarrow \infin} \sqrt[n]{| a_n |}$存在  
>  
> 根据极限的运算法则 $\lim\limits_{n \rightarrow \infin} \sqrt[n]{| a_n x^n |}$存在 且 $\lim\limits_{n \rightarrow \infin} \sqrt[n]{| a_n x^n |}$ = $\lim\limits_{n \rightarrow \infin} \sqrt[n]{| a_n |} \cdot \lim\limits_{n \rightarrow \infin} x$ = $\lim\limits_{n \rightarrow \infin} \sqrt[n]{| a_n |} \cdot x$  
>  
> ---
>
> 当|x| \< R 时    
>  
> $\lim\limits_{n \rightarrow \infin} \sqrt[n]{| a_n x^n |}$ = $\lim\limits_{n \rightarrow \infin} \sqrt[n]{| a_n |} \cdot x$ < $\lim\limits_{n \rightarrow \infin} \sqrt[n]{| a_n |} \cdot \frac{1}{\lim\limits_{n \rightarrow \infin} \sqrt[n]{| a_n |}}$ = 1  
> 不妨设$\lim\limits_{n \rightarrow \infin} \sqrt[n]{| a_n x^n |}$ = A 有 A < 1  
>   
> 我们有$\frac{1-\text{A}}{2}$ > 0  
> 根据极限的定义 取ϵ = $\frac{1-A}{2}$ > 0 存在H(ϵ) 当n > H(ϵ)时， $|\sqrt[n]{| a_n x^n |} - \text{A}|$ \< ϵ = $\frac{1-\text{A}}{2}$ 即 $\sqrt[n]{| a_n x^n |}$ < A + $\frac{1-\text{A}}{2}$ < $\frac{1}{2}$ + $\frac{\text{A}}{2}$ < 1    
> 取B = $\frac{1}{2}$ + $\frac{\text{A}}{2}$ 即 当n > H(ϵ)时 有$\sqrt[n]{| a_n x^n |}$ < B 且 B < 1 即 $| a_n x^n |$ < $\text{B}^n$ 且 B < 1  
>   
> 由于 几何级数${\displaystyle\sum_{n=0}^\infin} r^n$ 当r<1时 收敛  
> 根据 比较审敛法 $| a_n x^n |$收敛 即 $a_n x^n$绝对收敛 因此 $a_n x^n$收敛  
>  
> ---
>
> 当|x| \> R 时     
>  
> $\lim\limits_{n \rightarrow \infin} \sqrt[n]{| a_n x^n |}$ = $\lim\limits_{n \rightarrow \infin} \sqrt[n]{| a_n |} \cdot x$ > $\lim\limits_{n \rightarrow \infin} \sqrt[n]{| a_n |} \cdot \frac{1}{\lim\limits_{n \rightarrow \infin} \sqrt[n]{| a_n |}}$ = 1  
> 不妨设$\lim\limits_{n \rightarrow \infin} \sqrt[n]{| a_n x^n |}$ = A 有 A > 1  
> 
> 我们有$\frac{\text{A}-1}{2}$ > 0  
> 根据极限的定义 取ϵ = $\frac{\text{A}-1}{2}$ > 0 存在H(ϵ) 当n > H(ϵ)时， $|\sqrt[n]{| a_n x^n |} - \text{A}|$ \< ϵ = $\frac{1-\text{A}}{2}$ 即 $\sqrt[n]{| a_n x^n |}$ > A - $\frac{\text{A}-1}{2}$ < $\frac{1}{2}$ + $\frac{\text{A}}{2}$ > 1  
> 取B = $\frac{1}{2}$ + $\frac{\text{A}}{2}$ 即 当n > H(ϵ)时 有$\sqrt[n]{| a_n x^n |}$ > B 且 B > 1 即 $| a_n x^n |$ > $\text{B}^n$ > 1  
>  
> 取ϵ \< B 即能满足 $| a_n x^n |$ \> ϵ 因此 $\lim\limits_{n \rightarrow \infin} a_n x^n$ = 0不成立   
> 根据 级数收敛的必要条件 $a_n x^n$发散    

#### 指数函数（Exponential Functions）    
  
级数相乘  
//\[Rudin 1976\] / 3\.50 Theorem  
//\[陈天权 2009\] / 定理 3\.3\.6     
${\displaystyle\sum_{n=0}^\infin} a_n$ = A 且 ${\displaystyle\sum_{n=0}^\infin} a_n$绝对收敛 ${\displaystyle\sum_{n=0}^\infin} b_n$ = B ⇒ ${\displaystyle\sum_{n=0}^\infin} ({\displaystyle\sum_{k=0}^n} a_k b_{n-k})$ = C  
  
证明：  
> ${\displaystyle\sum_{j=0}^n} ({\displaystyle\sum_{k=0}^j} a_k b_{j-k})$  
= $a_0 b_0 + (a_0 b_1 + a_1 b_0) + ... +  (a_0 b_n + a_1 b_{n-1} + ... + a_n b_0)$  
= $a_0 ( b_0 + b_1 + ... + b_n ) + a_1 ( b_0 + b_1 ... + b_{n-1} ) + ... +  a_n b_0$  
= $a_0 ( b_0 + b_1 + ... + b_n ) + a_1 ( b_0 + b_1 ... + b_{n-1} ) + ... +  a_n b_0$   
= $a_0 {\displaystyle\sum_{j=0}^n} b_j + a_1 {\displaystyle\sum_{j=0}^{n-1}} b_j + ... +  a_n {\displaystyle\sum_{j=0}^0} b_j$   
>  
> 设$\beta_n = {\displaystyle\sum_{j=0}^n} b_j - B$  
上式 = $a_0(B + \beta_n) + a_1(B + \beta_{n-1}) + ... + a_n(B + \beta_0)$  
= $(a_0 + a_1 + ... + a_n)B + a_0\beta_n + a_1\beta_{n-1} + ... + a_n\beta_0$  
= $({\displaystyle\sum_{j=0}^n} a_j) \cdot B + a_0\beta_n + a_1\beta_{n-1} + ... + a_n\beta_0$  
>    
> 设$\gamma_n = a_0\beta_n + a_1\beta_{n-1} + ... + a_n\beta_0$ 下面证明$\lim\limits_{n \rightarrow \infin} \gamma_n = 0$  
>   
> 未完待续  
  
---  
  
指数函数定义： $\displaystyle \exp(x) = \sum_{n = 0}^{\infin} \frac{x^n}{n!} = 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + \frac{x^4}{4!} + ...$  
//\[Rudin 1976\] / 8\.6 Theorem  
//\[陈天权 2009\] / 定义 3\.5\.2     

---  
  
$\displaystyle \exp(x) \cdot \exp(y) = \exp(x + y)$  
//\[Rudin 1976\] / 8\.6 Theorem   
//\[陈天权 2009\] / 定理 3\.5\.2       
   
证明：  
> $\displaystyle \exp(x) \cdot \exp(y)$    
= $\displaystyle \sum_{n=0}^\infin (\sum_{k=0}^n \frac{x^k \cdot y^{n-k}}{k! \cdot (n-k)!})$  
= $\displaystyle \sum_{n=0}^\infin (\frac{1}{n!} \sum_{k=0}^n \frac{n! \cdot x^k \cdot y^{n-k}}{k! \cdot (n-k)!})$  
= $\displaystyle \sum_{n=0}^\infin (\frac{1}{n!} \sum_{k=0}^n C_n^k \cdot x^k \cdot y^{n-k})$    
= $\displaystyle \sum_{n=0}^\infin \frac{ {(x + y)}^n }{n!}$ //逆用二项式定理      
= $\displaystyle \exp(x + y)$  
  
---  
   
根据 指数函数定义 $\displaystyle \exp(0) = 1$  
   
根据 欧拉数定义 $\displaystyle \exp(1) = \sum_{n=0}^\infin \frac{1}{n!} = e$  
   
可以证明 对任意实数x 有 $\displaystyle \exp(x) =  e^x$  //证明从略  

#### 三角函数（Trigonometric Functions）    
  
余弦定义：$\displaystyle \cos(x) = \frac{\exp(ix) + \exp(-ix)}{2}$  
  
正弦定义：$\displaystyle \sin(x) = \frac{\exp(ix) - \exp(-ix)}{2 i}$  

$\displaystyle \exp(ix) = 1 + ix - \frac{x^2}{2!} - \frac{ix^3}{3!} + \frac{x^4}{4!} + ...$  //i -1 -i 1  

$\displaystyle \exp(-ix) = 1 -ix - \frac{x^2}{2!} + \frac{ix^3}{3!} + \frac{x^4}{4!} + ...$  //-i -1 i 1  

$\displaystyle \cos(x) = 1 - \frac{x^2}{2!} + \frac{x^4}{4!} + ...$  

$\displaystyle \sin(x) = x - \frac{x^3}{3!} + \frac{x^5}{5!} + ...$  
  
---  
   
Euler公式：$\displaystyle \exp(ix) = \cos(x) + i\sin(x)$   

//证明  
//根据定义   
//正弦定义×i + 余弦定义 即可得证  

Euler公式 与 余弦/正弦定义 等价  
可以 基于Euler公式 推出  余弦/正弦定义   
将-ix代入Euler公式后 得到 $\displaystyle \exp(-ix) = \exp(i(-x)) = \cos(-x) + i\sin(-x) = \cos(x) - i\sin(x)$  
与欧拉公式相加/减后 即可得到 余弦/正弦定义  
    
    
   
   
### 极限（limit）    

虽然 数列可以认为是一种特殊的函数  
但是 数列极限却不可以认为是一种特殊的函数极限 //在函数极限的定义中 要求函数在去心领域上有定义 而去心领域包含一段连续的实数 这是数列所不具备的   

去心领域 deleted neighborhood    
领域 neighborhood  
  
函数极限定义 //epsilon-delta definition   
$\forall \, \epsilon > 0 , \, \exists \, \delta > 0 , \, \forall \, 0 < |x - x_0| < \delta \, , \, |\operatorname{f}(x) - A| < \epsilon \Leftrightarrow \lim\limits_{x \rightarrow x_0} \operatorname{f}(x) = A$    
  
Sequential Criterion for Limits //函数极限与数列极限的关系 //Robert Bartle, Donald Sherbert. "Introduction to Real Analysis, Fourth Edition" 4.1.8 Theorem  
函数f(x)在x0处的极限为A 数列{xn}的极限为x0 且 存在N，当n>N时，有xn≠x0 -> 数列{f(xn)}的极限为A  

函数极限的局部有界性 //Robert Bartle, Donald Sherbert. "Introduction to Real Analysis, Fourth Edition" 4.1.8 Theorem  

极限运算法则  
根据定义求极限的效率太低，因此引入了极限运算法则，但是这也是出错的开始  

有界函数与无穷小的乘积是无穷小  //\[同济大学数学系 2014\] 第一章 函数与极限 / 第五节 极限运算法则 / 定理2  

商法则  //分母不能为0   
复合函数  //存在去心邻域 满足g(x)不等于极限  

有理整函数（polynomial function） 或 (代入后分母不等于零的)有理分式函数（rational function） 直接代入即极限 //为提供证明 后文会扩充到初等函数     
  
**根据极限定义易知 对函数进行的恒等变形（比如“约分”等）或比较大小（比如“有界函数与无穷小乘积”/“夹逼准则”等） 只要 存在某个去心邻域 能使相应的恒等变形或比较大小成立 即可**    

~~单调收敛原理/单调收敛定理（Monotone Convergence Theorem） 单调有界数列必有极限 //仅适用于数列 且不能求出极限的具体值~~    
  
夹逼准则（Squeeze Theorem） //由于效率较低，在求函数极限时，一般借助于初等函数的连续性，并不常用 //但求数列极限的方法较少，可能会用到夹逼准则  

~~柯西收敛准则 Cauchy's convergence test //柯西极限存在准则/柯西审敛原理~~  
            
---   
       
$\displaystyle \lim\limits_{x \rightarrow  0} \frac{\exp(x) - 1}{x} = 1$   
   
\[陈天权 2009\] / 例 3\.6\.2   
$\displaystyle \frac{\exp(x) - 1}{x}$  
= $\displaystyle \frac{(1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + \frac{x^4}{4!} + ...) - 1}{x}$    
= $\displaystyle 1 + \frac{x}{2!} + \frac{x^2}{3!} + \frac{x^3}{4!} + ...$  
= $\displaystyle 1 + x \cdot (\frac{1}{2!} + \frac{x}{3!} + \frac{x^2}{4!} + ...)$  
    
    
又 $\displaystyle  \lim\limits_{x \rightarrow 0} x = 0$ 是无穷小   
  
**根据极限定义易知 对函数进行的恒等变形（比如“约分”等）或比较大小（比如“有界函数与无穷小乘积”/“夹逼准则”等） 只要 存在某个去心邻域 能使相应的恒等变形或比较大小成立 即可**    
且 当0<|x-0|<1时 $\displaystyle | \frac{1}{2!} + \frac{x}{3!} + \frac{x^2}{4!} + ... |$ ≤ $\displaystyle | 1 + 1 + \frac{1}{2!} + \frac{1}{3!} + \frac{1}{5!} + ... |$ = e 有界 //严格意义上，应当对满足0<|x-0|<1的任意给定x，证明级数收敛（有界->正项级数收敛->绝对收敛->收敛），级数的值是关于x的函数 //并且函数又在0<|x-0|<1上有界        
    
因此 $\displaystyle  \lim\limits_{x \rightarrow 0} x \cdot (\frac{1}{2!} + \frac{x}{3!} + \frac{x^2}{4!} + ...) =0$ //有界函数与无穷小的乘积是无穷小        

$\displaystyle \lim\limits_{x \rightarrow 0} 1 + x \cdot (\frac{1}{2!} + \frac{x}{3!} + \frac{x^2}{4!} + ...) = 1$ //极限加法运算法则   

---    
       
$\displaystyle \lim\limits_{x \rightarrow  0} \frac{\sin(x) }{x} = 1$   
   
\[陈天权 2009\] / 例 3\.6\.4   
$\displaystyle \frac{\sin x}{x}$  
= $\displaystyle \frac{x - \frac{x^3}{3!} + \frac{x^5}{5!} + ...}{x}$  
= $\displaystyle 1 - \frac{x^2}{3!} + \frac{x^4}{5!} + ...$  
= $\displaystyle 1 + x^2 \cdot (- \frac{1}{3!} + \frac{x^2}{5!} + ...)$    
        
又 $\displaystyle  \lim\limits_{x \rightarrow 0} x^2 = 0$ 是无穷小   
    
**根据极限定义易知 对函数进行的恒等变形（比如“约分”等）或比较大小（比如“有界函数与无穷小乘积”/“夹逼准则”等） 只要 存在某个去心邻域 能使相应的恒等变形或比较大小成立 即可**      
且 当0<|x-0|<1时 $\displaystyle | - \frac{1}{3!} + \frac{x^2}{5!} + ... |$ ≤ $\displaystyle | 1 + 1 + \frac{1}{2!} + \frac{1}{3!} + \frac{1}{5!} + ... |$ = e 有界 //严格意义上，应当对满足0<|x-0|<1的任意给定x，证明级数收敛（有界->正项级数收敛->绝对收敛->收敛），级数的值是关于x的函数 //并且函数又在0<|x-0|<1上有界   

因此 $\displaystyle  \lim\limits_{x \rightarrow 0} x^2 \cdot (- \frac{1}{3!} + \frac{x^2}{5!} + ...) =0$ //有界函数与无穷小的乘积是无穷小   
  
$\displaystyle \lim\limits_{x \rightarrow 0} 1 + x^2 \cdot (- \frac{1}{3!} + \frac{x^2}{5!} + ...) = 1$ //极限加法运算法则    
   
      
---    
   
$\lim\limits_{x \rightarrow \infin} {( 1 + \frac{1}{x} )}^x = e$  
$=\lim\limits_{x \rightarrow \infin} e^{ ( \ln ( { ( 1 + \frac{1}{x} ) } ^ x ) ) }$  
$=\lim\limits_{x \rightarrow \infin} e^{ ( x \ln ( 1 + \frac{1}{x} ) ) }$  
$=\lim\limits_{x \rightarrow \infin} e^{ \frac{\ln ( 1 + \frac{1}{x} )}{\frac{1}{x}} }$  
$=\lim\limits_{x \rightarrow 0} e^{ \frac{\ln ( 1 + x )}{x} }$  
    
---

$\lim\limits_{x \rightarrow 0} \sqrt[n]{1 + x} = 1$    
证明   
$\lim\limits_{x \rightarrow 0} 1 = 1$  
$\lim\limits_{x \rightarrow 0} 1 = 1 + x$  
That for all x > 0,  1 < $\sqrt[n]{1 + x}$ < 1 + x implies $\lim\limits_{x \rightarrow 0^+} \sqrt[n]{1 + x} = 1$   
That for all -1 < x < 0, 1 + x < $\sqrt[n]{1 + x}$ < 1 implies $\lim\limits_{x \rightarrow 0^-} \sqrt[n]{1 + x} = 1$       

无穷小 infinitesimal  
  
等价无穷小代替 提升效率  
  
当$x \rightarrow 0$时 sinx ~ x  
  
当$x \rightarrow 0$时 tanx ~ x  
  
当$x \rightarrow 0$时 1 - cosx ~ 1/2x^2  
  
当$x \rightarrow 0$时 $\sqrt[n]{1 + x} - 1$ ~ $\frac{1}{n}$  
证明：  
根据等比数列求和：$1 + ... + {( \sqrt[n]{1 + x} )}^{n - 2} + {( \sqrt[n]{1 + x} )}^{n - 1} = \frac{1}{\sqrt[n]{1 + x} - 1} ( {( \sqrt[n]{1 + x} )}^{n} - 1 )$ //恒等变形需要存在某个去心邻域能使其成立   
  
$\lim\limits_{x \rightarrow 0} \frac{\sqrt[n]{1 + x} - 1}{\frac{x}{n}}$    
$=\lim\limits_{x \rightarrow 0} \frac{\frac{{\sqrt[n]{1 + x} )}^{n} - 1}{1 + ... + {( \sqrt[n]{1 + x} )}^{n - 2} + {( \sqrt[n]{1 + x} )}^{n - 1}}}{\frac{x}{n}}$  

等价无穷小具有传递性 //等价类  

### 连续（continuous）    

函数连续定义  
$\displaystyle \lim\limits_{x \rightarrow x_0} \operatorname{f}(x) = \operatorname{f}(x_0)$ ⇒ f(x)在$x_0$处连续     

连续函数的性质 //局部性质  

Sequential Criterion for Continuity //将数列看作函数 利用复合函数的连续性 //Robert Bartle, Donald Sherbert. "Introduction to Real Analysis, Fourth Edition" 5.1.3 Theorem     
函数f(x)在x0处的极限为A 且 函数f(x)在x0处连续 数列{xn}的极限为x0 -> 数列{f(xn)}的极限为A   
注：与极限时的区别在于， 不再有”存在N，当n>N时，有xn≠x0“的限制  

连续函数运算  

初等函数 elementary function    
  
常函数 constant function  
幂函数  power  
指数函数 exponential function  
对数函数 logarithm  
三角函数 trigonometric function  
反三角函数 inverse trigonometric function 

monomial 单项式  
polynomial function 多项式函数 / 有理整函数？     
rational function 分式函数 / 有理分式函数？ 

闭区间上连续函数的性质  
连续函数的性质 -> 函数在连续点处的局部性质  

有界性定理（Boundedness Theorem）在闭区间上连续的函数在该区间上有界 //Robert Bartle, Donald Sherbert. "Introduction to Real Analysis, Fourth Edition" 2011 5.3.2 Boundedness Theorem  
f(x)在\[a,b\]上连续 -> f(x)在\[a,b\]上有界   
\[陈天权 2009\] / 定理4.2.2  
> 证明   
>  
> 令 S = { y ∈ \[a,b\] : f(x)在\[a,y\]上有界 }  
f(x)在\[a,b\]上连续 -> f(x)在a上连续 -> a ∈ S -> S非空  
根据S的定义，显然 b是S的一个上界  
根据LUB公理 S有上确界 不妨设为ζ=supS  
>
> 下面证明f(x)在\[a,ζ\]上有界 //**注：由于无法排除上确界ζ等于上界b的可能 //如果为半开区间\[a,b)，那么 当ζ=b时 就不一定有f(x)在ζ处有连续，命题就不一定成立**     
>
> f(x)在a上连续 -> f(x)在a的某个邻域内有界 -> ζ > a  
b是S的一个上界 -> ζ \<= b  
a < ζ <= b -> ζ ∈ \[a,b\] -> f(x)在ζ上连续 //**注：如果为半开区间\[a,b)，那么 当ζ=b时 就不一定有f(x)在ζ处有连续**      
根据 函数极限的局部有界性 不妨设f(x)在(ζ - δ, ζ)上有界  
又f(x)连续 f(x)在(ζ - δ, ζ]上有界
>
> ζ是S的上确界 不妨取某个小于δ的ϵ 即ζ - e > ζ - δ 存在η ∈ S且η > ζ - e(> ζ - δ) 
η ∈ S -> f(x)在\[a,η\]上有界  
>
> 综上f(x)在\[a,η\]∪(ζ - δ, ζ\]上有界（且η > ζ - δ） -> f(x)在\[a,ζ\]上有界  
>
> 下面证明ζ=b  
>
> 反证法，假设ζ≠b 由于ζ<=b 必有ζ\<b  
由于f(x)在ζ上连续  
根据 函数极限的局部有界性 不妨设f(x)在(ζ, ζ+δ2)上有界  
取某个δ3<δ2 有f(x)在(ζ, ζ+δ3]上有界  
由于f(x)在\[a,ζ\]上有界 -> f(x)在\[a,ζ\]∪(ζ, ζ+δ3\]上有界 -> f(x)在\[a,ζ+δ3\]上有界  
因此ζ+δ3 ∈ S 而 ζ+δ3 > ζ 这与ζ是S的上确界矛盾 命题得证  

//**注：必须闭区间才能成立 比如f(x)=1/x在[-1,0)上连续 但在[-1,0)上无界**    

极值定理（Extreme Value Theorem）/最大值最小值定理 在闭区间上连续的函数在该区间上一定能取得它的最大值和最小值 //[Bartle 2011] / 5.3.4 Maximum-Minimum Theorem  
//\[陈天权 2009\] 定理 4.2.3  
> 证明
> 
> 证明最大值的情形 
>
> 根据有界性定理 f(x)在\[a, b\]上有界  
根据LUB公理 { f(x) : a \<= x \<= b }有上确界 不妨设为α  
> 
> 下面证明 ∃ x ∈ \[a, b\], f(x) = α  
>
> 反证法 假设 ∀ x ∈ \[a, b\], f(x) ≠ α  
由于α是上确界 我们有f(x) < α 
>
> 构造 g(x) = 1/(α - f(x))  
根据极限的运算法则 可以证明g(x)在[a, b\]上连续  
根据有界性定理 g(x)在[a, b\]上有界 不妨设 1/(α - f(x)) < M (M>0)   
由于f(x) < α 有f(x) < α - 1/M (M>0)   
因此 α - 1/M 是f(x)的一个上界 且 α - 1/M < α 这与α是上确界矛盾  
   
##### 一致连续性（Uniform Continuity） 


### 微分（Differential）/导数（Derivative）

洛必达法则（L'Hôpital's rule）   
     
     

### 测度 Measure    
     
---  
集函数 Set Function

集合环 Ring of Sets  
\[Rudin 1976\] / 11.1 Definition       
$\displaystyle \mathcal{R}$是集合环 ⇔ ∅∈$\displaystyle \mathcal{R}$ 且 $\displaystyle \mathcal{R}$对差集(Set Difference)封闭 且 $\displaystyle \mathcal{R}$对并集(Union)封闭    

由于 A ∩ B = A - (A - B)，我们有集合环对交集(Intersection)封闭

//可以用数学归纳法将并集推广到有限次 //Finite Union       

单位 Unit  
X是$\displaystyle \mathcal{R}$的单位 ⇔ X∈$\displaystyle \mathcal{R}$ 且 ∀A∈$\displaystyle \mathcal{R}$,A⊂X   

由于 ∀A∈$\displaystyle \mathcal{R}$,A⊂X ⇔ $\displaystyle \mathcal{R}$ ⊂ ℘(X)，上述命题又可写为 X是$\displaystyle \mathcal{R}$的单位 ⇔ X∈$\displaystyle \mathcal{R}$ 且 $\displaystyle \mathcal{R}$ ⊂ ℘(X)      

集合代数 Algebra of Sets   
\[Rudin 1976\] / 11.1 Definition       
$\displaystyle \mathcal{R}$是X上的集合代数 ⇔ $\displaystyle \mathcal{R}$是集合环 且 X是$\displaystyle \mathcal{R}$的单位    
   
等价定义  
$\displaystyle \mathcal{R}$是X上的集合代数 ⇔ X是$\displaystyle \mathcal{R}$的单位 且 $\displaystyle \mathcal{R}$对(相对于X的)补集(Complement)封闭 且 $\displaystyle \mathcal{R}$对并集封闭     
证明   
>   
> 1 ⇒ 2    
> 由于X是$\displaystyle \mathcal{R}$的单位，有X∈$\displaystyle \mathcal{R}$ 且 ∀A∈$\displaystyle \mathcal{R}$，A⊂X；又因为$\displaystyle \mathcal{R}$对差集封闭；因此，$\displaystyle \mathcal{R}$对补集封闭   
>     
> 2 ⇒ 1         
> 由于 A - B = $\displaystyle \complement_{X}$($\displaystyle \complement_{X}$A ∪ B)，又因为$\displaystyle \mathcal{R}$对补集和并集封闭；因此，$\displaystyle \mathcal{R}$对差集封闭    
>     
>              
    
   
     
---        
//σ(Sigma)      
   
σ-环 // σ-Ring //Sigma-Ring    
\[Rudin 1976\] / 11.1 Definition       
$\displaystyle \mathcal{R}$是σ-环 ⇔ $\displaystyle \mathcal{R}$是集合环 且 对可数并集(Countable Union)封闭 //可数即和自然数集等势 参见 集合的势/基数   
  

由于$\displaystyle \bigcup_{n \isin \N} A_n$ = $\displaystyle A_1 - \bigcap_{n \isin \N} (A_1 - A_n)$，我们有集合环对可数交集(Countable Intersection)封闭  

σ-代数 //σ-Algebra //Sigma-Algebra  
\[Rudin 1976\] / 11.1 Definition       
\[陈天权 2009\] / 定义 9.1.1     
$\displaystyle \mathcal{R}$是X上的σ-代数 ⇔ X是$\displaystyle \mathcal{R}$的单位 且 $\displaystyle \mathcal{R}$是σ-环 ⇔ $\displaystyle \mathcal{R}$是X上的集合代数 且 对可数并集(Countable Union)封闭   
    
//显然，∀集合X，有\{℘(X)是X上的σ-代数\}    

集函数 Set Function    
\[陈天权 2009\] / 第9章 测度 /序言
\[Rudin 1976\] / 11.1 Definition       
μ是$\displaystyle \mathcal{R}$上的集函数 ⇔ μ是$\displaystyle \mathcal{R}$到扩展实数集(R∪{−∞,+∞})的映射   

(有限)可加 //(Finitely) Additive  
\[陈天权 2009\] / 定义 9.1.2     
\[Rudin 1976\] / 11.2 Definition       
$\displaystyle \mathcal{R}$是集合代数 且 μ是$\displaystyle \mathcal{R}$上的集函数 ⇒ ( μ是(有限)可加集函数 ⇔ ∀\"不相交(Disjoint)集合A,B∈$\displaystyle \mathcal{R}$\"，有\"μ(A ∪ B) = μ(A) +  μ(B)\" ) //可以用数学归纳法推广到有限次      

可数可加/σ-可加     
\[陈天权 2009\] / 定义 9.2.3     
\[Rudin 1976\] / 11.2 Definition  
$\displaystyle \mathcal{R}$是σ-代数 且 μ是$\displaystyle \mathcal{R}$上的集函数 ⇒ ( μ是可数可加集函数 ⇔ ∀\"两两不相交(Pairwise Disjoint)集合$\displaystyle A_1$,$\displaystyle A_2$,... ∈ $\displaystyle \mathcal{R}$\"，有\"μ($\displaystyle \bigcup_{n \isin \N} A_n$) = $\displaystyle \sum_{n \isin \N}$μ($\displaystyle A_n$)\" )     

//图形学中的立体角可以看作集函数     

//概率测度   
//概率论中的 概率密度函数 可以看作集函数 //加法原理    
\[陈天权 2009\] / 例 9.1.3                      
   
---  
外测度

外测度 //outer/exterior measure   
\[Rudin 1976\] / 11.8 Theorem  
\[陈天权 2009\] / 定义 9.3.1    
μ是X上的外测度 ⇔ μ是℘(X)到非负扩展实数集(\[0,+∞\])的映射 且 μ(∅) = 0 且 ∀\"集合A,B ∈ ℘(X) 满足 A ⊂ B\"，有\"μ(A) ≤ μ(B)\" \/\*单调性(Monotone)\*\/ 且 ∀\"集合$\displaystyle A_1$,$\displaystyle A_2$,... ∈ ℘(X)\"，有\"μ($\displaystyle \bigcup_{n \isin \N} A_n$) ≤ $\displaystyle \sum_{n \isin \N}$μ($\displaystyle A_n$)\" \/\*次可数可加性(Countable Subadditivity)\*\/    

//显然，∀集合X，有\"℘(X)是X上的σ-代数\" //关于定义中μ的定义域          
       
等价定义    
μ是X上的外测度 ⇔ μ是℘(X)到非负扩展实数集(\[0,+∞\])的映射 且 μ(∅) = 0 且 ∀\"集合A,$\displaystyle B_1$,$\displaystyle B_2$,... ∈ ℘(X) 满足 A ⊂ $\displaystyle \bigcup_{n \isin \N} B_n$\"，有\"μ(A) ≤ $\displaystyle \sum_{n \isin \N}$μ($\displaystyle B_n$)\"     
      
证明   
> 2 ⇒ 1   
> 取 $\displaystyle B_1$=B $\displaystyle B_2$,... =∅ 即可得到 ∀\"集合A,B ∈ ℘(X) 满足 A ⊂ B\"，有\"μ(A) ≤ μ(B)\"   
> 显然，由于$\displaystyle \bigcup_{n \isin \N} B_n$ ⊂ $\displaystyle \bigcup_{n \isin \N} B_n$，取 A=$\displaystyle \bigcup_{n \isin \N} B_n$, 有\"μ($\displaystyle \bigcup_{n \isin \N} A_n$) ≤ $\displaystyle \sum_{n \isin \N}$μ($\displaystyle A_n$)\"   
>     
> 1 ⇒ 2   
>  ∀\"集合A,B ∈ ℘(X) 满足 A ⊂ $\displaystyle \bigcup_{n \isin \N} B_n$\"，有\"    
> μ(A) ≤ μ($\displaystyle \bigcup_{n \isin \N} B_n$) //∀\"集合A,B ∈ ℘(X) 满足 A ⊂ B\"          
> μ($\displaystyle \bigcup_{n \isin \N} B_n$) ≤ $\displaystyle \sum_{n \isin \N}$μ($\displaystyle B_n$) //∀\"集合$\displaystyle A_1$,$\displaystyle A_2$,... ∈ $\displaystyle \mathcal{R}$\"      
> 即 μ(A) ≤ μ($\displaystyle \bigcup_{n \isin \N} B_n$) ≤ $\displaystyle \sum_{n \isin \N}$μ($\displaystyle B_n$)    
> \"        
>     
     
覆盖  
//覆盖的定义并不依赖于拓扑   
//见紧空间  
C = { $\displaystyle U_\alpha$ | α ∈ A } ⇒ ( C是Y的覆盖 ⇔ Y ⊂ $\displaystyle \bigcup_{\alpha \isin A} U_\alpha$ )    
//本质上来讲，定义中的指标集(Index Set)可以忽略， 理解为"Y 包含于 C中所有的元素的并集"即可 //即Y ⊂ $\displaystyle \bigcup_{U \isin C}$U    

构造外测度 //Construction of Outer Measure       
\[Rudin 1976\] / 11.7 Definition    
\[陈天权 2009\] / 引理 9.3.1    
Y ⊂ ℘(X) 且 ∅ ∈ Y 且 p是Y到非负扩展实数集(\[0,+∞\])的映射 且 p(∅)=0 且 φ的定义域为 ℘(X) 且 φ(E) = $\displaystyle \begin{cases} \displaystyle \inf \{ \sum_{A \isin C} \operatorname{p} ( A ) \, | \, C \text{是} \text{可数集} \, \text{且} \, C \text{是} E \text{的覆盖} \, \text{且} C \subset Y \} & \displaystyle \text{当} \, \exist \text{"} C \text{","} C \text{是} \text{可数集} \, \text{且} \, C \text{是} E \text{的覆盖} \, \text{且} \, C \subset Y \text{"} \, \text{时} \\ +\infty & \displaystyle \text{当} \, \nexists \text{"} C \text{","} C \text{是} \text{可数集} \, \text{且} \, C \text{是} E \text{的覆盖} \, \text{且} \, C \subset Y \text{"} \, \text{时} \end{cases}$ ⇒ φ是X上的外测度     
//关于φ(E)，可以理解为 所有可能的"包含于Y且覆盖E的可数集C" "C中的所有的元素在P中的像的累加"   

证明 
> 
> 由于 p(∅)=0 且 p非负，显然 φ(∅)=0  
> 
> ∀ \"集合A,B ∈ ℘(X) 满足 A ⊂ B\"，有\"显然 { $\displaystyle \sum_{D \isin C}$p(D) | C是可数集 且 C是A的覆盖 且 C ⊂ Y } ⊂ { $\displaystyle \sum_{D \isin C}$p(D) | C是可数集 且 C是B的覆盖 且 C ⊂ Y }     
> 根据下确界的定义，显然 φ(A) ≤ φ(B)\"
>   
> ∀ \"集合$\displaystyle S_1$,$\displaystyle S_2$,... ∈ ℘(X)\"，有\" 如果 ∃ \' n ∈ $\displaystyle \N$ \'，满足 \' ∄ C是可数集 且 C是$\displaystyle S_n$的覆盖 且 C ⊂ Y \'，那么 ∄ C是可数集 且 C是$\displaystyle \bigcup_{i \isin \N} S_i$的覆盖 且 C ⊂ Y，从而 φ($\displaystyle S_n$)=+∞ 且 φ($\displaystyle \bigcup_{i \isin \N} S_i$)=+∞，从而 φ($\displaystyle \bigcup_{i \isin \N} S_i$) ≤ $\displaystyle \sum_{i \isin \N}$φ($\displaystyle S_i$)成立   
>  
> 下面讨论 ∀ \' n ∈ $\displaystyle \N$ \'，有 \' ∃ C是可数集 且 C是$\displaystyle S_n$的覆盖 且 C ⊂ Y \' 的情形   
> ∀ \' ε > 0 \'，有\'   
> ∀\'n ∈ $\displaystyle \N$\'，有\'将 正实数=$\displaystyle \frac{\varepsilon}{2^{1+n}}$ 应用到下确界的定理，得到 ∃\'M ∈ { $\displaystyle \sum_{A \isin C}$p(A) | C是可数集 且 C是$\displaystyle S_n$的覆盖 且 C ⊂ Y }\'满足\'M < φ($\displaystyle S_n$) + $\displaystyle \frac{\varepsilon}{2^{n+1}}$\'   
> 不妨将M记作$\displaystyle C_n$(强调与n的关联)，即 ∃ \'$\displaystyle C_n$是可数集 且 $\displaystyle C_n$是$\displaystyle S_n$的覆盖 且 $\displaystyle C_n$ ⊂ Y 且 $\displaystyle \sum_{A \isin C_n}$p(A) < φ($\displaystyle S_n$) + $\displaystyle \frac{\varepsilon}{2^{n+1}}$\' //一说此处的证明涉及到选择公理 \'    
> 从而，记K=$\displaystyle \bigcup_{n \isin \N} C_n$，有 K是可数集 且 K是$\displaystyle \bigcup_{n \isin \N} S_n$的覆盖 且 K ⊂ Y，从而 $\displaystyle \sum_{A \isin K}$p(A) ⊂ { $\displaystyle \sum_{A \isin C}$p(A) | C是可数集 且 C是$\displaystyle \bigcup_{n \isin \N} S_n$的覆盖 且 C ⊂ Y }   
> 根据φ的定义和下确界的定义，有 φ($\displaystyle \bigcup_{n \isin \N} S_n$) ≤ $\displaystyle \sum_{A \isin K}$p(A)    
> 由于 A∈K则一定有A∈某个$\displaystyle C_n$ 且 p非负，有$\displaystyle \sum_{A \isin K}$p(A) ≤ $\displaystyle \sum_{n \isin N} \sum_{A \isin C_n} \operatorname{p} (A)$   
> 又根据上文中已证明的结论，$\displaystyle \sum_{n \isin N} \sum_{A \isin C_n} \operatorname{p} (A)$ ≤ $\displaystyle \sum_{n \isin N} \displaystyle$ ( φ($\displaystyle S_n$) + $\displaystyle \frac{\varepsilon}{2^{n+1}}$ )，根据等比数列求和 $\displaystyle \sum_{n \isin N} \displaystyle$ ( φ($\displaystyle S_n$) + $\displaystyle \frac{\varepsilon}{2^{n+1}}$ ) ≤ $\displaystyle \sum_{n \isin N} \displaystyle$ φ($\displaystyle S_n$) + ε  
\'  
> 即 ∀ \' ε > 0 \'，有\' φ($\displaystyle \bigcup_{n \isin \N} S_n$) ≤ $\displaystyle \sum_{n \isin N} \displaystyle$ φ($\displaystyle S_n$) + ε \'，从而 φ($\displaystyle \bigcup_{n \isin \N} S_n$) ≤ $\displaystyle \sum_{n \isin N} \displaystyle$ φ($\displaystyle S_n$) \" //注： 根据\" ∀ \'ε > 0\'，有\'a ≤ b + ε\' \" 可以得出 \" a ≤ b \" //用反证法即可证明，假设 a > b，取 ε = $\displaystyle \frac{a-b}{2}$ > 0 即可得出矛盾    
>    
   
---   
卡拉西奥多里 //Caratheodory     

卡拉西奥多里准则(Caratheodory's Criterion) //可测性(Measurability)   
\[陈天权 2009\] / 定义 9.4.1    
μ是X上的外测度 且 E ⊂ X ⇒ ( E是μ-可测的(μ-measurable) ⇔ ∀\"A ⊂ X\",有\"μ(A) = μ(A ∩ E) + μ(A ∩ $\displaystyle \complement_{X}$E)\" ) 

//一说\"μ(A) = μ(A ∩ E) + μ(A − E)\" //可以理解为用E将A“分割”开       

注：由于A = (A ∩ E) ∪ (A ∩ $\displaystyle \complement_{X}$E)，根据外侧度的定义(次可数可加性)，∀\"A ⊂ X\",有\"μ(A) ≤ μ(A ∩ E) + μ(A ∩ $\displaystyle \complement_{X}$E)\" 一定成立；因此，上述定义的等价形式为∀\"A ⊂ X\",有\"μ(A) ≥ μ(A ∩ E) + μ(A ∩ $\displaystyle \complement_{X}$E)\"   
  
注意，并集和差集并不能简单的理解成加法和减法    
B ∪ (A − B) = A ∪ B 而非 = A //可以直接从集合的定义证明，相等于证明 ∀\"a ∈ B ∪ (A − B)\"，有\"a ∈ A ∪ B\" 且 ∀\"a ∈ A ∪ B\"，有\"a ∈ B ∪ (A − B)\"       

可测集构成σ-代数 //Measurable Sets form Sigma-Algebra   
\[Rudin 1976\] / 11.10 Theorem  
\[陈天权 2009\] / 定理 9.4.1       
\[Yeh 2014\] / Theorem 2.8    
μ是X上的外测度 且 M = { E | E ⊂ X 且 E是μ-可测的 } ⇒ M是σ-代数    
      
证明      
>    
> 显然 μ(A ∩ X) = μ(X) 且 μ(A ∩ $\displaystyle \complement_{X}$X) = μ(A ∩ ∅) = μ(∅) = 0，有 μ(X) = μ(A ∩ X) + μ(A ∩ $\displaystyle \complement_{X}$X)，从而 X ∈ M //X是M的单位       
> 
> 对任意 E ∈ M，根据 卡拉西奥多里准则 的定义，显然 有$\displaystyle \complement_{X}$E ∈ M //M对补集封闭   
>        
> 对任意 E ∈ M，F ∈ M，     
> μ(A) \= μ(A ∩ E) + μ(A ∩ $\displaystyle \complement_{X}$E) //将A = A且E = E应用到定义"卡拉西奥多里准则"      
> \= ( μ(A ∩ E ∩ F) + μ(A ∩ E ∩ $\displaystyle \complement_{X}$F) ) + μ(A ∩ $\displaystyle \complement_{X}$E) //将A = A ∩ E且E = F应用到定义"卡拉西奥多里准则"          
> \= μ(A ∩ E ∩ F) + μ(A ∩ E ∩ $\displaystyle \complement_{X}$F) + ( μ(A ∩ $\displaystyle \complement_{X}$E ∩ F) + μ(A ∩ $\displaystyle \complement_{X}$E ∩ $\displaystyle \complement_{X}$F) ) //将A = A ∩ $\displaystyle \complement_{X}$E且E = F应用到定义"卡拉西奥多里准则"   
> ≥ μ(A ∩ (E ∪ F)) + μ(A ∩ $\displaystyle \complement_{X}$E ∩ $\displaystyle \complement_{X}$F) //因为(E ∩ F)∪(E ∩ $\displaystyle \complement_{X}$F)∪($\displaystyle \complement_{X}$E ∩ F) = E ∪ F，又根据外侧度的定义(次可数可加性)    
> \= μ(A ∩ (E ∪ F)) + μ(A ∩ $\displaystyle \complement_{X}$(E ∪ F))   
> 即 E ∪ F ∈ M //根据上文，由于≤一定成立，因此≥是=的充分必要条件(等价形式) //M对并集封闭    
>  
> 下面证明对可数并集封闭   
> 对任意 $\displaystyle E_1$ ∈ M，$\displaystyle E_2$ ∈ M，...， //尝试证明$\displaystyle \bigcup_{n \isin \N } E_n$ ∈ M          
>           
> 使用数学归纳法可以将对并集封闭推广到有限次，从而 $\displaystyle \bigcup_{i = 0}^{n} E_i$ ∈ M //数学归纳法可以推广到有限次而不能推广到可数次的原因不明，可能涉及到更高深的数学知识     
> 对任意 n ∈ $\displaystyle \N$，有 μ(A) = μ(A ∩ $\displaystyle \bigcup_{i = 0}^{n} E_i$) + μ(A - $\displaystyle \bigcup_{i = 0}^{n} E_i$) //M的定义 //(可测性)定义"卡拉西奥多里准则"     
> ≥ μ(A ∩ $\displaystyle \bigcup_{i = 0}^{n} E_i$) + μ(A - $\displaystyle \bigcup_{n \isin \N } E_n$) //外侧度的定义(单调性)   
> \= μ(A ∩ $\displaystyle \bigcup_{i = 0}^{n} E_i$) - μ(A ∩ $\displaystyle \bigcup_{i = 0}^{n-1} E_i$) + μ(A ∩ $\displaystyle \bigcup_{i = 0}^{n-1} E_i$) - μ(A ∩ $\displaystyle \bigcup_{i = 0}^{n-2} E_i$) + ... + μ(A ∩ $\displaystyle \bigcup_{i = 0}^{0} E_i$) - μ(A ∩ ∅) + μ(A - $\displaystyle \bigcup_{n \isin \N } E_n$) //裂项级数(Telescoping Series)    
> \= $\displaystyle \sum_{i=0}^{n}$(μ(A ∩ $\displaystyle \bigcup_{k = i}^{n} E_k$) - μ(A ∩ $\displaystyle \bigcup_{k = i}^{n-1} E_k$)) + μ(A - $\displaystyle \bigcup_{n \isin \N } E_n$) //裂项级数(Telescoping Series)       
> \= $\displaystyle \sum_{i=0}^{n}$(μ(A ∩ $\displaystyle \bigcup_{k = i}^{n} E_k$) - μ(A ∩ $\displaystyle \bigcup_{k = i}^{n} E_k$ ∩ $\displaystyle \bigcup_{k = i}^{n-1} E_k$)) + μ(A - $\displaystyle \bigcup_{n \isin \N } E_n$) //因为$\displaystyle \bigcup_{k = i}^{n-1} E_k$ ⊂ $\displaystyle \bigcup_{k = i}^{n} E_k$               
> \= $\displaystyle \sum_{i=0}^{n}$μ((A ∩ $\displaystyle \bigcup_{k = i}^{n} E_k$) − $\displaystyle \bigcup_{k = i}^{n-1} E_k$) + μ(A - $\displaystyle \bigcup_{n \isin \N } E_n$) //将A = A ∩ $\displaystyle \bigcup_{k = i}^{n} E_k$且E = $\displaystyle \bigcup_{k = i}^{n-1} E_k$应用到定义"卡拉西奥多里准则，有μ((A ∩ $\displaystyle \bigcup_{k = i}^{n} E_k$) = μ(A ∩ $\displaystyle \bigcup_{k = i}^{n} E_k$ ∩ $\displaystyle \bigcup_{k = i}^{n-1} E_k$)) + μ((A ∩ $\displaystyle \bigcup_{k = i}^{n} E_k$) − $\displaystyle \bigcup_{k = i}^{n-1} E_k$)      
> \= $\displaystyle \sum_{i=0}^{n}$μ(A ∩ ($\displaystyle \bigcup_{k = i}^{n} E_k$ − $\displaystyle \bigcup_{k = i}^{n-1} E_k$)) + μ(A - $\displaystyle \bigcup_{n \isin \N } E_n$)    
>      
> 由于对任意n ∈ $\displaystyle \N$成立，因此，在n趋向于$\displaystyle +\infty$时也成立，有 //\"n趋向于$\displaystyle +\infty$\"的这波操作在定义上可能缺乏严谨性，可能涉及到更高深的数学知识                   
> μ(A) ≥ $\displaystyle \sum_{i = 0 \land i \isin \N}^{+\infty}$μ(A ∩ ($\displaystyle \bigcup_{k = i}^{n} E_k$ − $\displaystyle \bigcup_{k = i}^{n-1} E_k$)) + μ(A - $\displaystyle \bigcup_{n \isin \N } E_n$)  
> ≥ μ(A ∩ (($\displaystyle \bigcup_{k = i \land k \isin \N}^{+\infty} E_k$ − $\displaystyle \bigcup_{k = i \land k \isin \N}^{+\infty-1} E_k$) ∪...∪($\displaystyle \bigcup_{k = i}^{0} E_k$ − ∅))) + μ(A - $\displaystyle \bigcup_{n \isin \N } E_n$)    
> \= μ(A ∩ $\displaystyle \bigcup_{n \isin \N} E_n$) + μ(A - $\displaystyle \bigcup_{n \isin \N } E_n$)     
> 从而 $\displaystyle \bigcup_{n \isin \N } E_n$ ∈ M //根据上文，由于≤一定成立，因此≥是=的充分必要条件(等价形式) //M对可数并集封闭       
>  

\[陈天权 2009\] / 定理 9.4.1       
\[Yeh 2014\] / Theorem 2.9  
μ是X上的外测度 且 M = { E | E ⊂ X 且 E是μ-可测的 } ⇒ u在M上可数可加    
    
证明      
>     
> 下面证明有限可加     
> 对任意 不相交的 E ∈ M，F ∈ M， //不相交即E ∩ F = ∅   
> 将A = E ∪ F且E = E应用到卡拉西奥多里准则，有μ(E ∪ F) = μ(E ∪ F ∩ E) + μ(E ∪ F ∩ $\displaystyle \complement_{X}$E)     
> 显然有E ∪ F ∩ E = E 又由于E和F不相交，有E ∪ F ∩ $\displaystyle \complement_{X}$E=F   
> 即μ(E ∪ F)= μ(E) + μ(F)     
> 
> 下面证明可数可加           
> 对任意 两两不相交(Pairwise Disjoint)集合$\displaystyle E_1$,$\displaystyle E_2$,... ∈ M，     
> 对任意 n ∈ $\displaystyle \N$，有   
> μ($\displaystyle \bigcup_{i \isin \N } E_i$) ≥ μ($\displaystyle \bigcup_{i=0 \land i \isin \N }^{n} E_i$) //外侧度的定义(单调性)       
> \= $\displaystyle \sum_{i=0 \land i \isin \N}^{n}$μ($\displaystyle E_i$)     
>    
> 由于对任意n ∈ $\displaystyle \N$成立，因此，在n趋向于$\displaystyle +\infty$时也成立，有 //\"n趋向于$\displaystyle +\infty$\"的这波操作在定义上可能缺乏严谨性，可能涉及到更高深的数学知识              
> μ($\displaystyle \bigcup_{i \isin \N } E_i$) ≥ $\displaystyle \sum_{i \isin \N}$μ($\displaystyle E_i$)    
> 从而μ($\displaystyle \bigcup_{i \isin \N } E_i$) = $\displaystyle \sum_{i \isin \N}$μ($\displaystyle E_i$) //根据上文，由于≤一定成立，因此≥是=的充分必要条件(等价形式)      
>   


卡拉西奥多里扩张定理(Caratheodory's Extension Theorem)     

---   
与度量空间(Metric Space)相关联   

博雷尔代数 Borel Algebra     
   
博雷尔集 Borel Set        

              
### 积分 Integral         
     
定积分/黎曼积分 Riemann Integral   
反常积分/广义积分  Henstock–Kurzweil Integral/Generalized Riemann Integral    
     
#### 换元积分法 Integration by Substitution    
     
##### 第一类换元法 //凑微分法       
设g(x)可以写成g(x)=f\[φ(x)\]φ'(x)的形式    
有$\displaystyle \int_a^b g(x) \, dx = \int_{\operatorname{\phi}(a)}^{\operatorname{\phi}(b)} f(u) \, du$    
即$\displaystyle \int_a^b g(x) \, dx = \int_a^b f[\operatorname{\phi}(x)]\operatorname{\phi}'(x) \, dx = {[\int_{\phi(a)}^{\phi(b)} f(u) \, du]}_{}$      
  
> 证明    
> 设F(u)是f(u)的原函数    
> 有$\displaystyle \int_{\phi(a)}^{\phi(b)} f(u) \, du$ = F\[φ(b)\] - F\[φ(a)\] （等式1）    
>           
> 设G(x)=F\[φ(x)\]     
> **有G'(x)=F'\[φ(x)\]φ'(x)=f\[φ(x)\]φ'(x) ⇒ 因此G(x)是g(x)的原函数** //证明的关键     
> $\displaystyle \int_a^b g(x) \, dx$ = G(b) - G(a) = F\[φ(b)\]  - F\[φ(a)\] （等式2）
> 
> 结合（等式1）（等式2），我们有$\displaystyle \int_a^b g(x) \, dx = \int_{\phi(a)}^{\phi(b)} f(u) \, du$，命题得证  
   
##### 第二类换元法 //变量代换法   
设φ(a)=α、φ(b)=β、u=φ(x)可导      
有$\displaystyle \int_{\alpha}^{\beta} f(u) \, du = \int_a^b f(\operatorname{\phi}(t))\operatorname{\phi}'(t) \, dt$    
即$\displaystyle \int_{\alpha}^{\beta} f(u) \, du = \int_{{\operatorname{\phi}}^{-1}(\alpha)}^{{\operatorname{\phi}}^{-1}(\beta)} f(\operatorname{\phi}(t))\operatorname{\phi}'(t) \, dt$    

> 证明    
> 设F(u)是f(u)的原函数      
> 有$\displaystyle \int_{\alpha}^{\beta} f(u) \, du$ = F(β) - F(α) （等式1）     
>           
> 设G(x)=F\[φ(x)\]      
> **有G'(x)=F'\[φ(x)\]φ'(x)=f\[φ(x)\]φ'(x) ⇒ 因此G(x)是f\[φ(x)\]φ'(x)的原函数** //证明的关键      
> $\displaystyle \int_a^b f(\operatorname{\phi}(t))\operatorname{\phi}'(t) \, dt$ = G(b) - G(a) = F\[φ(b)\]  - F\[φ(a)\] = F(β) - F(α) （等式2）        
>      
> 结合（等式1）（等式2），我们有$\displaystyle \int_{\alpha}^{\beta} f(u) \, du = \int_a^b f(\operatorname{\phi}(t))\operatorname{\phi}'(t) \, dt$，命题得证   
   
#### 分部积分法 Integration by Parts    


### 参考文献  
\[Bartle 2011\] Robert Bartle, Donald Sherbert. "Introduction to Real Analysis, Fourth Edition." Wiley 2011.   
\[Rudin 1976\] Walter Rudin. "Principles of Mathematical Analysis, Third Edition." McGraw-Hill 1976.    
\[Yeh 2014\] James Yeh. "Real Analysis: Theory of Measure and Integration, Third Edition." World Scientific 2014
\[同济大学数学系 2014\] 同济大学数学系. "高等数学 第七版." 高等教育出版社 2014.    
\[陈天权 2009\] 陈天权. "数学分析讲义." 北京大学出版社 2009.  
