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
    
---       

\[定义\] 拓扑(Topology) / 拓扑空间(Topological Space)           
\[陈天权 2009\] / 定义 7\.1\.1       
\[Yeh 2014\] / \[IV\] Borel σ-algebras //σ(Sigma)          
(X,τ)是拓扑空间 ⇔ τ是X上的拓扑 ⇔ τ ⊂ ℘(X) 且 ∅ ∈ τ 且 X ∈ τ 且 τ对无限并封闭 且 τ对有限交封闭 //此处的无限并没有要求可数 //可数即和自然数集等势 参见 集合的势/基数           

//用于不强调τ的情形     
X是拓扑空间 ⇔ ∃τ, (X,τ)是拓扑空间 ⇔ ∃τ, τ是X上的拓扑               

\[定义\] 开集(Open Set) // 拓扑(Topology)         
\[陈天权 2009\] / 定义 7\.1\.1       
\[Yeh 2014\] / \[IV\] Borel σ-algebras //σ(Sigma)                   
(X,τ)是拓扑空间 ⇒ ( U是开集 ⇔ U ∈ τ )        

//用于不强调τ的情形      
X是拓扑空间 ⇔ ( U是开集 ⇔ ∃τ, (X,τ)是拓扑空间 且 U ∈ τ )    

//开集对无限并封闭 开集对有限交封闭   

开集/闭集的概念源于对R上的开区间/闭区间的抽象      
无限个开区间的交可能是闭区间 比如：$\displaystyle \bigcap_{n \isin \N} (1-\frac{1}{n}, 2+\frac{1}{n})$=\[1,2\] //根据定义即可证明 //可能用到反证法       
        
\[定理\] \[等价定义\] 开集(Open Set) //通过 内部(Interior) //开集的内部是开集自身   
//ProofWiki / Interior of Open Set   
X是拓扑空间 且 S ⊂ X 且 $\displaystyle \text{S} \degree$是S的内部 ⇒ ( S是开集 ⇔ $\displaystyle \text{S} \degree$ = S )         

> 证明  
>   
> 1 ⇒ 2   
> 由于S是(包含于S的)开集，而$\displaystyle \text{S} \degree$是所有(包含于S的)开集的并集，因此S ⊂ $\displaystyle \text{S} \degree$ //\[定理\] S的内部是(包含于S的)最大开集     
> 根据内部的定义，由于定义中的每个A都有A ⊂ S，显然，并集$\displaystyle \bigcup \text{A}$即S的内部$\displaystyle \text{S} \degree$，一定有$\displaystyle \text{S} \degree$ ⊂ S       
> 因此$\displaystyle \text{S} \degree$ = S   
>
> 2 ⇒ 1  
> 根据开集的定义，开集对无限并封闭，因此$\displaystyle \text{S} \degree$是开集   
> 由于$\displaystyle \text{S} \degree$ = S，因此S是开集    
>         
        
\[定理\] \[等价定义\] 开集(Open Set) //通过 内点(Interior Point)    
\[陈天权 2009\] / 命题 7\.1\.1   
\[Rudin 1976\] / 2.18 Definition (f)   
ProofWiki / Set is Open iff Neighborhood of all its Points           
X是拓扑空间 ⇒ ( S是开集 ⇔ ∀"p ∈ S","p是S的内点" ) //S是开集 当且仅当 任何S中的点都是S的内点    
> 证明   
> 
> 根据 "\[定理\] \[等价定义\] 内点 Interior Point //通过 内部(Interior)"，有 p是S的内点 ⇔ p ∈ $\displaystyle \text{S} \degree$  
> 根据 "\[定理\] \[等价定义\] 开集 Open Set //通过 内部(Interior)"，有 S是开集 ⇔ $\displaystyle \text{S} \degree$ = S     
> 从而 ∀"p ∈ S","p是S的内点" ⇔ ∀"p ∈ S","p ∈ $\displaystyle \text{S} \degree$" ⇔ S = $\displaystyle \text{S} \degree$ ⇔ S是开集                     
>     
    
---    
      
\[定义\] 闭集(Closed Set)    
\[陈天权 2009\] / 定义 7\.1\.4      
X是拓扑空间 且 S ⊂ X ⇒ ( S是闭集 ⇔ X − S 是开集 )                 
       
//闭集对有限并封闭 闭集对无限交封闭 //可以用德摩根定律(De Morgan's laws)证明      
//(X上的离散拓扑)∅和X既是开集又是闭集 //可以用德摩根定律(De Morgan's laws)证明      
            
\[定理\] \[等价定义\] 闭集(Open Set) //通过 闭包(Closure) //闭集的闭包是闭集自身    
//ProofWiki / Set is Closed iff Equals Topological Closure      
X是拓扑空间 且 S ⊂ X 且 $\displaystyle \overline{\text{S}}$是S的闭包 ⇒ ( S是闭集 ⇔ $\displaystyle \overline{\text{S}}$ = S )         

> 证明  
>   
> 1 ⇒ 2 / 证法1  
> 由于S是(包含S的)闭集，而$\displaystyle \overline{\text{S}}$是所有(包含S的)闭集的交集，因此$\displaystyle \overline{\text{S}}$ ⊂ S //\[定理\] S的闭包是(包含S的)最小闭集     
> 根据闭包的定义，由于定义中的每个A都有S ⊂ A，显然，交集$\displaystyle \bigcap \text{A}$即S的闭包$\displaystyle \overline{\text{S}}$，一定有S ⊂ $\displaystyle \overline{\text{S}}$       
> 因此$\displaystyle \overline{\text{S}}$ = S   
>     
> 1 ⇒ 2 / 证法2      
> 设S'是S的导集，有 S' ⊂ S //根据 "\[定理\] \[等价定义\] 闭集(Closed Set) //通过 导集(Derived Set)"    
> 根据集合的定义，S' ⊂ S ⇔ S ∪ S' = S //ProofWiki / Union with Superset is Superset  
> 又因为$\displaystyle \overline{\text{S}}$ = S ∪ S' //根据 "\[定理\] \[等价定义\] 闭包(Closure) //通过 导集(Derived Set)"      
> 从而$\displaystyle \overline{\text{S}}$ = S       
>
> 2 ⇒ 1  
> 根据闭集的定义(和德摩根定律)，闭集对无限交封闭，因此$\displaystyle \overline{\text{S}}$是闭集   
> 由于$\displaystyle \overline{\text{S}}$ = S，因此S是闭集    
>       

\[定理\] \[等价定义\] 闭集(Closed Set) //通过 导集(Derived Set)      
X是拓扑空间 且 S ⊂ X ⇒ ( S是闭集 ⇔ S'是S的导集 且 S' ⊂ S )                 
ProofWiki / Equivalence of Definitions of Closed Set     
> 证明 //参考 \[陈天权 2009\] / 命题 7\.1\.2            
>      
> 1 ⇒ 2     
> ∀"p ∈ X","p $\displaystyle \notin$ S ⇔ p ∈ (X − S) ⇒ ∃"$\displaystyle \text{U}_p$=(X − S),$\displaystyle \text{U}_p$是p的开领域","S ∩ ( $\displaystyle \text{U}_p$ − {p} ) = ∅" ⇒ p不是S的极点 ⇔ p $\displaystyle \notin$ S'"       
> 根据逆否命题等价，∀"p ∈ X","p ∈ S' ⇒ p ∈ S"，由于S' ⊂ X，从而S' ⊂ S       
>       
> 2 ⇒ 1          
> 由于S' ⊂ S 且 S' ⊂ X， ∀"p ∈ X","p ∈ S' ⇒ p ∈ S"      
> 根据逆否命题等价，∀"p ∈ X","p $\displaystyle \notin$ S ⇒ p $\displaystyle \notin$ S'"      
> 从而 ∀"p ∈ X","p ∈ (X − S) ⇔ p $\displaystyle \notin$ S ⇒ p $\displaystyle \notin$ S' ⇔ p不是S的极点 ⇔ ∃"$\displaystyle \text{U}_p$,$\displaystyle \text{U}_p$是p的开领域","S ∩ ( $\displaystyle \text{U}_p$ − {p} ) = ∅" ⇒ ∃"$\displaystyle \text{U}_p$,$\displaystyle \text{U}_p$是p的开领域","$\displaystyle \text{U}_p$ ⊂ (X − S)" ⇒ p是(X − S)的内点"     
> 因此(X − S)是开集 //根据 "\[定理\] \[等价定义\] 开集 Open Set //通过 内点(Interior Point)"         
> 从而S是闭集                
>      

---      
          
\[定义\] 领域 Neighborhood         
\[陈天权 2009\] / 定义 7\.1\.3    
\[Rudin 1976\] / 2.18 Definition (a)     
X是拓扑空间 且 p ∈ X ⇒ ( V是p的领域 ⇔ V ⊂ X 且 ∃"U","U是开集 且 p ∈ U 且 U ⊂ V" )      
      
\[定义\] 开领域 Open Neighbourhood    
\- \[Tu 2011\] / Definition A.1 //   
\- ProofWiki / Definition:Neighborhood (Topology)/Neighborhood defined as Open
\[陈天权 2009\] / 定义 7\.1\.3      
X是拓扑空间 且 p ∈ X ⇒ ( V是p的开领域 ⇔  V是x的领域 且 V是开集 ) //即 ∃"V","V是开集 且 p ∈ V"      
        
---                                          
          
\[定义\] 内点(Interior Point)     
\[陈天权 2009\] / 定义 7\.1\.3       
\[Rudin 1976\] / 2.18 Definition (e)     
X是拓扑空间 且 p ∈ X 且 S ⊂ X ⇒ ( p是S的内点 ⇔ ∃"$\displaystyle \text{U}_p$","$\displaystyle \text{U}_p$是p的开领域 且 $\displaystyle \text{U}_p$ ⊂ S" )  

\[定理\] \[等价定义\] 内点(Interior Point) //通过 内部(Interior)         
X是拓扑空间 且 p ∈ X 且 S ⊂ X 且 $\displaystyle \text{S} \degree$是S的内部 ⇒ ( p是S的内点 ⇔ p ∈ $\displaystyle \text{S} \degree$ )   
> 证明  //参考\[陈天权 2009\] / 命题 7\.1\.1     
>      
> 1 ⇒ 2      
> 根据内点和开领域的定义，有 ∃"$\displaystyle \text{U}_p$","$\displaystyle \text{U}_p$是开集 且 p ∈ $\displaystyle \text{U}_p$ 且 $\displaystyle \text{U}_p$ ⊂ S"，即 $\displaystyle \text{U}_p$是包含于S的开集     
> 由于$\displaystyle \text{S} \degree$是所有(包含于S的)开集的并集，有$\displaystyle \text{U}_p$ ⊂ $\displaystyle \text{S} \degree$ //\[定理\] S的内部是(包含于S的)最大开集   
> 从而 p ∈ $\displaystyle \text{S} \degree$ 
>    
> 2 ⇒ 1     
> 由于$\displaystyle \text{S} \degree$是开集 且 $\displaystyle \text{S} \degree$ ⊂ S /\* 根据内部的定义 \*/，从而 ∃"$\displaystyle \text{U}_p$ = $\displaystyle \text{S} \degree$","$\displaystyle \text{U}_p$是开集 且 p ∈ $\displaystyle \text{S} \degree$ 且  $\displaystyle \text{S} \degree$ ⊂ S"，即 $\displaystyle \text{U}_p$是p的开领域 且 $\displaystyle \text{U}_p$ ⊂ S         
> 从而 p是S的内点    
>  
         
---    
   
(集合的)极点(Limit Point (of Set)) / 聚点(Cluster Point / Accumulation Point)    
X是拓扑空间 且 p ∈ X 且 S ⊂ X ⇒ ( p是S的聚点 ⇔ ∀"$\displaystyle \text{U}_p$,$\displaystyle \text{U}_p$是p的开领域","S ∩ ( $\displaystyle \text{U}_p$ − {p} ) ≠ ∅" )     
//其中 $\displaystyle \text{U}_p$ − {p} 具体化后即 去心领域(Deleted Neighborhood)    
//ProofWiki / Definition:Limit Point/Topology/Set        
//\[陈天权 2009\] / 定义 7\.1\.6      
//\[Rudin 1976\] / 2.18 Definition (b)        
      
---    
      
孤立点(Isolated Point)   
X是拓扑空间 且 p ∈ X 且 S ⊂ X ⇒ ( p是S的孤立点 ⇔ p ∈ S 且 ∃"$\displaystyle \text{U}_p$","$\displaystyle \text{U}_p$是p的开领域 且 S ∩ ( $\displaystyle \text{U}_p$ − {p} ) = ∅" )      
//即p ∈ S 且 p不是S的聚点 S      
//值得注意的是，在内点/极点/孤立点的定义中，只有孤立点要求p ∈ S，内点要求p ∈ X但要求$\displaystyle \text{U}_p$ ⊂ S，而极点只要求p ∈ X           
\[陈天权 2009\] / 定义 7\.1\.6   
\[Rudin 1976\] / 2.18 Definition (c)   
     
---       
     
附着点(Adherent Point)    
X是拓扑空间 且 p ∈ X 且 S ⊂ X ⇒ ( p是S的附着点 ⇔ ∀"$\displaystyle \text{U}_p$,$\displaystyle \text{U}_p$是p的开领域","S ∩ $\displaystyle \text{U}_p$ ≠ ∅" )         
//显然，附着点不是极点就是孤立点 //可以认为极点和孤立点统称为附着点             

\[定理\] \[等价定义\] 附着点(Adherent Point) //通过 闭包(Closure)         
X是拓扑空间 且 p ∈ X 且 S ⊂ X 且 $\displaystyle \overline{\text{S}}$是S的闭包 ⇒ ( p是S的附着点 ⇔ p ∈ $\displaystyle \overline{\text{S}}$ )         
\[陈天权 2009\] / 命题 7\.1\.2       
> 证明     
> 根据附着点的定义，相当于证明  ∀"p ∈ X","∀"$\displaystyle \text{U}_p$,$\displaystyle \text{U}_p$是p的开领域","S ∩ $\displaystyle \text{U}_p$ ≠ ∅" ⇔ p ∈ $\displaystyle \overline{\text{S}}$"      
> 
> 1 ⇒ 2              
> 相当于证明逆否命题 ∀"p ∈ X","p $\displaystyle \notin$ $\displaystyle \overline{\text{S}}$ ⇒ ∃"$\displaystyle \text{U}_p$,$\displaystyle \text{U}_p$是p的开领域","S ∩ $\displaystyle \text{U}_p$ = ∅""    
> ∀"p ∈ X","p $\displaystyle \notin$ $\displaystyle \overline{\text{S}}$ ⇒ p ∈ (X - $\displaystyle \overline{\text{S}}$) ⇒ ∃"$\displaystyle \text{U}_p$ = (X - $\displaystyle \overline{\text{S}}$),$\displaystyle \text{U}_p$是p的开领域","S ∩ $\displaystyle \text{U}_p$ = ∅""    
>           
> 2 ⇒ 1      
> 相当于证明逆否命题 ∀"p ∈ X"," ∃"$\displaystyle \text{U}_p$,$\displaystyle \text{U}_p$是p的开领域","S ∩ $\displaystyle \text{U}_p$ = ∅" ⇒ p $\displaystyle \notin$ $\displaystyle \overline{\text{S}}$"                
> 由于 ∃"$\displaystyle \text{U}_p$,$\displaystyle \text{U}_p$是p的开领域","S ∩ $\displaystyle \text{U}_p$，根据闭集的定义，(X - $\displaystyle \text{U}_p$)是闭集，因此 p $\displaystyle \notin$ (X - $\displaystyle \text{U}_p$) 且 (X - $\displaystyle \text{U}_p$)是包含S的闭集    
> 由于 $\displaystyle \overline{\text{S}}$是所有包含S的闭集的交，根据交集的定义，从而 p $\displaystyle \notin$ $\displaystyle \overline{\text{S}}$               
>    
    
---  

边界点(Boundary Point)         
X是拓扑空间 且 p ∈ X 且 S ⊂ X ⇒ ( p是S的边界点 ⇔ ∀"$\displaystyle \text{U}_p$,$\displaystyle \text{U}_p$是p的开领域","S ∩ $\displaystyle \text{U}_p$ ≠ ∅ 且 (X − S) ∩ $\displaystyle \text{U}_p$ ≠ ∅" )          
     
\[定理\] \[等价定义\] 边界点(Boundary Point) //通过 边界(Boundary)         
X是拓扑空间 且 p ∈ X 且 S ⊂ X 且 $\displaystyle \partial \text{S}$是S的边界 ⇒ ( p是S的边界点 ⇔ p ∈ $\displaystyle \partial \text{S}$ )           
//ProofWiki / Equivalence of Definitions of Boundary     
> 证明       
> ∀"$\displaystyle \text{U}_p$,$\displaystyle \text{U}_p$是p的开领域","S ∩ $\displaystyle \text{U}_p$ ≠ ∅" ⇔ p是S的附着点 ⇔ p ∈  $\displaystyle \overline{\text{S}}$ //根据 "\[定理\] \[等价定义\] 附着点(Adherent Point) //通过 闭包(Closure)"    
> ∀"$\displaystyle \text{U}_p$,$\displaystyle \text{U}_p$是p的开领域","(X − S) ∩ $\displaystyle \text{U}_p$ ≠ ∅" ⇔ p是S的附着点 ⇔ p ∈  $\displaystyle \overline{\text{X} - \text{S}}$ //根据 "\[定理\] \[等价定义\] 附着点(Adherent Point) //通过 闭包(Closure)"           
> 从而，p是S的附着点 ⇔ p ∈ $\displaystyle \overline{\text{S}}$ ∩ $\displaystyle \overline{\text{X} - \text{S}}$ ⇔ p ∈ $\displaystyle \partial \text{S}$ //根据 "\[定理\] \[等价定义\] 边界(Boundary) //通过 闭包(Closure)"                                   
>                       
          
---            
             
\[定义\] 内部(Interior) //S的内部是所有(包含于S的)开集的并集           
X是拓扑空间 且 S ⊂ X ⇒ ( $\displaystyle \text{S} \degree$是S的内部 ⇔ $\displaystyle \text{S} \degree$ = $\displaystyle \bigcup_{\text{A} \isin \mathcal{A}} \text{A}$ 且 $\displaystyle \mathcal{A}$ = \{ A | A是开集 且 A ⊂ S \} )       
\[陈天权 2009\] / 定义 7\.1\.7    
       
\[定理\] \[等价定义\] 内部(Interior) //S的内部是(包含于S的)最大开集      
X是拓扑空间 且 S ⊂ X ⇒ ( $\displaystyle \text{S} \degree$是S的内部 ⇔ $\displaystyle \text{S} \degree$ ⊂ S 且 $\displaystyle \text{S} \degree$是开集 且 ∀"A是开集 且 A ⊂ S","A ⊂ $\displaystyle \text{S} \degree$" )      
//ProofWiki / Set Interior is Largest Open Set //Obsolete      
//ProofWiki / Equivalence of Definitions of Interior           
> 证明  
>     
> 1 ⇒ 2    
> 由于A ∈ $\displaystyle \mathcal{A}$一定有A ⊂ S，根据并集的定义，一定有$\displaystyle \text{S} \degree$ ⊂ S      
> 根据开集的定义，开集对无限并封闭，因此$\displaystyle \text{S} \degree$是开集    
> 如果A是开集 且 A ⊂ S，那么一定有A ∈ $\displaystyle \mathcal{A}$，根据并集的定义，一定有A ⊂ S$\displaystyle \degree$，因此$\displaystyle \text{S} \degree$最大。                
> 
> 2 ⇒ 1          
> 不妨设H是S的内部，有H = $\displaystyle \bigcup_{\text{A} \isin \mathcal{A}} \text{A}$ 且 $\displaystyle \mathcal{A}$ = \{ A | A是开集 且 A ⊂ S \}   
> 由于$\displaystyle \text{S} \degree$是开集 且 $\displaystyle \text{S} \degree$ ⊂ S，因此，S ∈ $\displaystyle \mathcal{A}$，根据并集的定义，一定有$\displaystyle \text{S} \degree$ ⊂ H    
> 根据开集的定义，开集对无限并封闭，因此H是开集，并且由于A ∈ $\displaystyle \mathcal{A}$一定有A ⊂ S，根据并集的定义，一定有H ⊂ S，由于$\displaystyle \text{S} \degree$是(包含于S的)最大开集，因此H ⊂ $\displaystyle \text{S} \degree$      
> 从而$\displaystyle \text{S} \degree$ = H，即$\displaystyle \text{S} \degree$是S的内部    
>    
      
\[定理\] \[等价定义\] 内部(Interior) //通过 内点(Interior Point) //S内部是由所有S的内点构成的集合            
X是拓扑空间 且 S ⊂ X ⇒ (  $\displaystyle \text{S} \degree$是S的内部 ⇔ $\displaystyle \text{S} \degree$ = { p | p是S的内点 } )                 
//根据 "\[定理\] \[等价定义\] 内点 Interior Point //通过 内部(Interior)" 显然            
       
\[定理\] \[等价定义\] 内部(Interior) //通过 闭包(Closure)         
X是拓扑空间 且 S ⊂ X 且 $\displaystyle \text{S} \degree$是S的内部 且 $\displaystyle \overline{\text{S}}$是S的闭包 ⇒  $\displaystyle \text{S} \degree$ = $\displaystyle \text{X} - \overline{\text{X} - \text{S}}$    
//ProofWiki / Interior equals Complement of Closure of Complement   
//ProofWiki / Complement of Interior equals Closure of Complement   
//根据对称性 显然     
//可以用德摩根定律证明     

---       

\[定义\] 导集(Derived Set)    
\[陈天权 2009\] / 定义 7\.1\.6   
\[Rudin 1976\] / 2.26 Definition
X是拓扑空间 且 S ⊂ X ⇒ ( S'是S的导集 ⇔ S' = { p | p是S的聚点 }  

---    
       
\[定义\] 闭包(Closure) //S的闭包是所有(包含S的)闭集的交集  
\[陈天权 2009\] / 定义 7\.1\.5      
\[Rudin 1976\] / 2\.27 Theorem         
X是拓扑空间 且 S ⊂ X ⇒ ( $\displaystyle \overline{\text{S}}$是S的闭包 ⇔ $\displaystyle \overline{\text{S}}$ = $\displaystyle \bigcap_{\text{A} \isin \mathcal{A}} \text{A}$ 且 $\displaystyle \mathcal{A}$ = \{ A | A是闭集 且 S ⊂ A \} )         
    
\[定理\] \[等价定义\] 闭包(Closure) //S的闭包是(包含S的)最小闭集      
X是拓扑空间 且 S ⊂ X ⇒ ( $\displaystyle \overline{\text{S}}$是S的闭包 ⇔ S ⊂ $\displaystyle \overline{\text{S}}$ 且 $\displaystyle \overline{\text{S}}$是闭集 且 ∀"A是闭集 且 S ⊂ A","$\displaystyle \overline{\text{S}}$ ⊂ A" )     
//ProofWiki / Set Closure is Smallest Closed Set/Topology    
//ProofWiki / Equivalence of Definitions of Closure of Topological Subspace   
> 证明  
>     
> 1 ⇒ 2    
> 由于A ∈ $\displaystyle \mathcal{A}$一定有S ⊂ A，根据交集的定义，一定有S ⊂ $\displaystyle \overline{\text{S}}$      
> 根据闭集的定义，闭集对无限交封闭，因此$\displaystyle \overline{\text{S}}$是闭集    
> 如果A是闭集 且 S ⊂ A，那么一定有A ∈ $\displaystyle \mathcal{A}$，根据交集的定义，一定有$\displaystyle \overline{\text{S}}$ ⊂ A，因此$\displaystyle \overline{\text{S}}$最小。                
> 
> 2 ⇒ 1          
> 不妨设H是S的闭包，有H = $\displaystyle \bigcap_{\text{A} \isin \mathcal{A}} \text{A}$ 且 $\displaystyle \mathcal{A}$ = \{ A | A是闭集 且 S ⊂ A \}         
> 由于$\displaystyle \overline{\text{S}}$是闭集 且  S ⊂ $\displaystyle \overline{\text{S}}$，因此 $\displaystyle \overline{\text{S}}$ ∈ $\displaystyle \mathcal{A}$，根据交集的定义，一定有H ⊂ $\displaystyle \overline{\text{S}}$    
> 根据闭集的定义，闭集对无限交封闭，因此H是闭集，并且由于A ∈ $\displaystyle \mathcal{A}$一定有S ⊂ A，根据交集的定义，一定有S ⊂ H，由于$\displaystyle \overline{\text{S}}$是(包含S的)最小闭集，因此$\displaystyle \overline{\text{S}}$ ⊂ H      
> 从而$\displaystyle \overline{\text{S}}$ = H，即$\displaystyle \overline{\text{S}}$是S的闭包    
>   

\[定理\] \[等价定义\] 闭包(Closure) //通过 附着点(Adherent Point) //S闭包是由所有S的附着点构成的集合       
X是拓扑空间 且 S ⊂ X ⇒ ( $\displaystyle \overline{\text{S}}$是S的闭包 ⇔ $\displaystyle \overline{\text{S}}$ = { p | p是S的附着点 } )      
//根据 "\[定理\] \[等价定义\] 附着点(Adherent Point) //通过 闭包(Closure)" 显然                
   
\[定理\] \[等价定义\] 闭包(Closure) //通过 导集(Derived Set)      
X是拓扑空间 且 S ⊂ X 且 $\displaystyle \overline{\text{S}}$是S的闭包 且 S'是S的导集 ⇒ $\displaystyle \overline{\text{S}}$ = S ∪ S'                
\[陈天权 2009\] / 定义 7\.1\.6   
\[Rudin 1976\] / 2\.26 Definition     
ProofWiki / Equivalence of Definitions of Closure of Topological Subspace / 1 ⇒ 6          
> 证明     
>            
> 由于      
> $\displaystyle \overline{\text{S}}$ = \{ p | ∀"$\displaystyle \text{U}_p$,$\displaystyle \text{U}_p$是p的开领域","S ∩ $\displaystyle \text{U}_p$ ≠ ∅" \} //根据 "\[定理\] \[等价定义\] 闭包(Closure) //通过 附着点(Adherent Point)"    
> S = \{ p | {p} ∩ S ≠ ∅ \} //显然  
> S' = \{ p | ∀"$\displaystyle \text{U}_p$,$\displaystyle \text{U}_p$是p的开领域","S ∩ ( $\displaystyle \text{U}_p$ − {p} ) ≠ ∅" \} //根据 聚点 和 导集 的定义  
>   
> 显然 命题成立    
>     
            
---  
    
\[定义\] 边界(Boundary)  
X是拓扑空间 且 S ⊂ X 且 $\displaystyle \partial \text{S}$是S的边界 ⇒ $\displaystyle \partial \text{S}$ = $\displaystyle \overline{\text{S}}$ − $\displaystyle \text{S} \degree$          
\[陈天权 2009\] / 定义 7\.1\.8       
   
\[定理\] \[等价定义\] 边界(Boundary) //通过 闭包(Closure)     
X是拓扑空间 且 S ⊂ X 且 $\displaystyle \partial \text{S}$是S的边界 ⇒ $\displaystyle \partial \text{S}$ = $\displaystyle \overline{\text{S}}$ ∩ $\displaystyle \overline{\text{X} - \text{S}}$              
//由于闭包是闭集合，又因为闭集对无限交封闭，从而边界是闭集        
> 证明       
> 由于 $\displaystyle \overline{\text{X} - \text{S}}$ = X − $\displaystyle \text{S} \degree$ //根据 "\[定理\] \[等价定义\] 内部(Interior) //通过 闭包(Closure)"         
>               
> 从而，$\displaystyle \overline{\text{S}}$ ∩ $\displaystyle \overline{\text{X} - \text{S}}$ = $\displaystyle \overline{\text{S}}$ ∩ ( X − $\displaystyle \text{S} \degree$ ) = $\displaystyle \overline{\text{S}}$ − $\displaystyle \text{S} \degree$ = $\displaystyle \partial \text{S}$                 
>       

\[定理\] \[等价定义\] 边界(Boundary) //通过 内部(Interior)     
X是拓扑空间 且 S ⊂ X 且 $\displaystyle \partial \text{S}$是S的边界 ⇒ $\displaystyle \partial \text{S}$ = X − ( $\displaystyle \text{S} \degree$ ∪ $\displaystyle ( \text{X} - \text{S} ) \degree$ )      
> 证明    
> 由于       
> $\displaystyle \overline{\text{X} - \text{S}}$ = X − $\displaystyle \text{S} \degree$ //根据 "\[定理\] \[等价定义\] 内部(Interior) //通过 闭包(Closure)"            
> $\displaystyle \overline{\text{X} - (\text{X} - \text{S})}$ = X − $\displaystyle ( \text{X} - \text{S} ) \degree$ //根据 "\[定理\] \[等价定义\] 内部(Interior) //通过 闭包(Closure)"              
> $\displaystyle \partial \text{S}$ = $\displaystyle \overline{\text{S}}$ ∩ $\displaystyle \overline{\text{X} - \text{S}}$ //根据 "\[定理\] \[等价定义\] 边界(Boundary) //通过 闭包(Closure)"     
>         
> 从而，X − ( $\displaystyle \text{S} \degree$ ∪ $\displaystyle ( \text{X} - \text{S} ) \degree$ ) = ( X − $\displaystyle \text{S} \degree$ ) ∪ ( X − $\displaystyle ( \text{X} - \text{S} ) \degree$ ) = $\displaystyle \overline{\text{X} - \text{S}}$ ∪ $\displaystyle \overline{\text{X} - (\text{X} - \text{S})}$ = $\displaystyle \overline{\text{X} - \text{S}}$ ∪ $\displaystyle \overline{\text{S}}$ = $\displaystyle \partial \text{S}$    
>    


\[定理\]    
X是拓扑空间 且 S ⊂ X ⇒ ( S是开集且S是闭集 ⇔ $\displaystyle \partial S$ = ∅ )                    
> 证明     
>        
> 1 ⇒ 2    
> S是开集 且 S是闭集 ⇒ S = $\displaystyle \overline{\text{S}}$ 且 S = $\displaystyle \text{S} \degree$ ⇒ $\displaystyle \partial \text{S}$ = $\displaystyle \overline{\text{S}}$ − $\displaystyle \text{S} \degree$ = ∅       
>     
> 2 ⇒ 1   
> $\displaystyle \partial \text{S}$ = ∅ ⇒ $\displaystyle \overline{\text{S}}$ − $\displaystyle \text{S} \degree$ = ∅ ⇒  $\displaystyle \overline{\text{S}}$ = $\displaystyle \text{S} \degree$    
> 又因为 $\displaystyle \text{S} \degree$ ⊂ S ⊂ $\displaystyle \overline{\text{S}}$    
> 从而 $\displaystyle \overline{\text{S}}$ = $\displaystyle \text{S} \degree$ ⊂ S ⊂ $\displaystyle \overline{\text{S}}$ = $\displaystyle \text{S} \degree$ 有 $\displaystyle \overline{\text{S}}$ ⊂ S 且 S ⊂ $\displaystyle \text{S} \degree$                     
> 从而 S = $\displaystyle \overline{\text{S}}$ 且 S = $\displaystyle \text{S} \degree$  因此 S是开集 且 S是闭集    
>         

### Compactness 紧性     

\[Definition\] Cover of Set 覆盖  
\- \[Tu 2011\] / A.8 Compactness  
\- ProofWiki / Definition:Cover of Set  
\- ProofWiki / Definition:Set Union/Set of Sets  
$\displaystyle \mathcal{C}$ is a cover of S ⇔ S ⊂ $\displaystyle \bigcup_{\displaystyle U \isin \mathcal{C}} \text{U}$  
//覆盖的定义并不依赖于拓扑  

\[定义\] 子覆盖(Subcover)     
C是Y的覆盖 ⇒ ( D是C关于Y的子覆盖 ⇔ D是Y的覆盖 且 D ⊂ C )                
//ProofWifi / Definition:Subcover       
//\[陈天权 2009\] / 定义 7\.6\.1               
//子覆盖的定义并不依赖于拓扑     
            
\[定义\] 有限子覆盖(Finite Subcover)     
C是Y的覆盖 ⇒ ( D是C关于Y的有限子覆盖 ⇔ D是C关于Y的子覆盖 且 D是有限集 )      
//ProofWifi / Definition:Subcover/Finite      
//\[陈天权 2009\] / 定义 7\.6\.1       
//有限子覆盖的定义并不依赖于拓扑         
            
\[定义\] 开覆盖(Open Cover)    
X是拓扑空间 且 Y ⊂ X ⇒ ( C是Y的(在X上的)开覆盖 ⇔ C是Y的覆盖 且 ∀"A ∈ C","A是(在X上的)开集" )      
//\[陈天权 2009\] / 定义 7\.6\.1       
              
---         
      
\[定义\] 紧的(Compact) //紧的(Compact) ⇔ 有限的(Finite) //从(有限或无限)开覆盖C中**选择**有限个开集(C的元素)来覆盖Y             
X是拓扑空间 且 Y ⊂ X ⇒ ( K(在X上)是紧的 ⇔ ∀C : C是Y的(在X上的)开覆盖 ⇒ ( ∃ F : F是C关于K的有限子覆盖 ) )         
//ProofWiki / Definition:Compact Space/Topology/Subspace         
//\[陈天权 2009\] / 定义 7\.6\.1        
//\[Rudin 1976\] / 2\.31 Definition       
       
\[定理\] 有限的 ⇒ 紧的     
X是拓扑空间 且 Y ⊂ X ⇒ ( Y是有限集 ⇒ Y是紧集 )     
//ProofWiki /Finite Topological Space is Compact       
//根据紧集的定义，显然 //一说涉及到选择公理     

\[定理\] 紧(Compact)集的子集 ⇒ ( 闭集 ⇒ 紧的 )    
//ProofWiki / Closed Subspace of Compact Space is Compact     
//\[Browder 1996\] / 6.52 Proposition   
//\[陈天权 2009\] / 定义 7\.6\.3              

---    
              
\[定义\] 收敛序列(Convergent Sequence) //拓扑空间中的序列极限       
X是拓扑空间 且 Y ⊂ X 且 $\displaystyle {\lang x_n \rang}_{ n \isin \N }$是Y上的无限序列 ⇒ ( $\displaystyle {\lang x_n \rang}_{ n \isin \N }$(在X上)收敛于a ⇔ ( a ∈ X 且 ∀$\displaystyle \text{U}_a$ : $\displaystyle \text{U}_a$是a的(在X上的)开领域 ⇒ ( ∃ N > 0 : ∀ n > N : $\displaystyle x_n$ ∈ $\displaystyle \text{U}_a$ ) ) )            
//ProofWiki / Definition:Convergent Sequence/Topology         
//\[Tu 2011\] / Definition A.54   
//\[陈天权 2009\] / 定义 7\.5\.1        

//(序列的)极(限)点(Limit Point(of Sequence)) //注意与聚点的定义区分           
X是拓扑空间 且 Y ⊂ X 且 $\displaystyle {\lang x_n \rang}_{ n \isin \N }$是Y上的无限序列 ⇒ ( $\displaystyle {\lang x_n \rang}_{ n \isin \N }$(在X上)收敛于a ⇔ a是$\displaystyle {\lang x_n \rang}_{ n \isin \N }$(在X上)(当n趋于无穷时的)极(限)点 )                 
          
---             
                 
\[定理\] 序列引理(The sequence lemma) //(序列的)极(限)点 ⇒ 附着点（即在闭包内）//个人认为可以在拓扑空间中成立，并不依赖于度量空间         
X是拓扑空间 且 $\displaystyle {\lang x_n \rang}_{ n \isin \N }$是S上的无限序列 且 S ⊂ X 且 $\displaystyle {\lang x_n \rang}_{ n \isin \N }$(在X上)收敛于a ⇒ a是S的附着点 //即a在闭包内                   
//ProofWiki / Closure of Subset of Metric Space by Convergent Sequence       
//\[Tu 2011\] / Definition A.56   
//\[陈天权 2009\] / 命题 7\.5\.2       
> 证明                   
> 根据拓扑空间中序列收敛的定义，∀$\displaystyle \text{U}_a$ : $\displaystyle \text{U}_a$是a的(在X上的)开领域 ⇒ ( ∃ N > 0 : ∀ n > N : $\displaystyle x_n$ ∈ $\displaystyle \text{U}_a$ ) ⇒ $\displaystyle \text{U}_a$ ∩ S ≠ ∅ //由于$\displaystyle {\lang x_n \rang}_{ n \isin \N }$是S上的无限序列 至少有$\displaystyle x_n$(当n > N时) ∈ $\displaystyle \text{U}_a$ ∩ S                
> 根据附着点的定义，a是S的附着点                 
> 根据"\[定理\] \[等价定义\] 闭包(Closure) //通过 附着点(Adherent Point)"，a ∈ $\displaystyle \overline{\text{S}}$              
>            
              
---
        
\[定义\] 列紧的(Sequentially Compact)              
X是拓扑空间 且 Y ⊂ X ⇒ ( Y(在X上)是列紧的 ⇔ ( ∀$\displaystyle {\lang x_n \rang}_{ n \isin \N }$是Y上的无限序列 : ∃ $\displaystyle {\lang x_{n_k} \rang}_{ k \isin \N }$是$\displaystyle {\lang x_n \rang}_{ n \isin \N }$的子列 : ∃ a ∈ Y : $\displaystyle {\lang x_{n_k} \rang}_{ k \isin \N }$(在X上)收敛于a ) )          
//ProofWiki / Definition:Sequentially Compact Space        
//\[陈天权 2009\] / 定义 7\.6\.5      
//子列(Subsequence)     

波尔查诺-魏尔斯特拉斯定理 Bolzano-Weierstrass Theorem        

魏尔施特拉斯逼近定理 Weierstrass Approximation Theorem           

斯通-魏尔施特拉斯定理 Stone-Weierstrass Theorem                              

### Subspace Topology 子空间拓扑 / Relative Topology 相对拓扑

\[Definition\] Definition:Topological Subspace 拓扑子空间                      
\- \[Tu 2011\] / A.2 Subspace Topology     
\- ProofWifi / Definition:Topological Subspace   
\- \[陈天权 2009\] / 定义 7\.4\.1   
\- \[Browder 1996\] / 6.26 Definition           
(X, τ) is topological space ∧ A ⊂ X ⇒ ( (A, $\displaystyle \text{τ}_A$) is a topological subspace of(X,τ) ⇔ $\displaystyle \text{τ}_A$ is a subspace topology on A ( induced by τ ) ⇔ $\displaystyle \text{τ}_A$ = { U ∩ A : U ∈ τ } ) // induce 诱导   
//显然，根据拓扑空间的定义可以证明，拓扑子空间是拓扑空间                  

\[Definition\] Definition:Relatively Open Set 相对开集  
\- \[Tu 2011\] / A.2 Subspace Topology       
\- ProofWifi / Definition:Relatively Closed Set   
\- Encyclopedia of Mathematics / Relatively-open (-closed) set  
(X, τ) is topological space ∧ (A, $\displaystyle \text{τ}_A$) is a topological subspace of(X,τ) ⇒ ( U is relatively open to/in A ⇔ ∃ open set V in X such that V ∩ A = U )  
// 根据定义，A中的相对开集与A中的开集并没有差别，但A中的相对开集往往暗示着不是X中的开集  
// 拓扑子空间中的开集并不一定是拓扑空间中的开集 //比如 \[0,1/2) = (-1/2, 1/2) ∩ \[0, 1\] 是 \[0, 1\]中的相对开集 但 并不是 R中的开集      
  
  
### Bases 基  
\- \[Tu 2011\] / A.3 Bases       

\[Definition\] Definition:Local Basis 局部基  
\- \[Tu 2011\] / Definition A.6  
\- ProofWiki / Definition:Local Basis/Local Basis for Open Sets  
S is topological space ⇒ ( $\displaystyle \mathcal{B}_p$ is a local basis at p (in S) ⇔ ∀ $\displaystyle \text{B}_p$ ∈ $\displaystyle \mathcal{B}_p$ : $\displaystyle \text{B}_p$ is an open neighborhood of p (in S) ∧ ∀ open neighborhood U of p (in S) : ∃ $\displaystyle \text{B}_p$ ∈ $\displaystyle \mathcal{B}_p$ such that $\displaystyle \text{B}_p$ ⊂ U )  
// a set of open neighborhood of p (in S) such that every open neighborhood of p (in S) contains some set in $\displaystyle \mathcal{B}_p$  

\[Definition\] Definition:Basis (Topology)/Analytic Basis 基  
\- ProofWiki / Definition:Basis (Topology)/Analytic Basis  
S is topological space ⇒ ( $\displaystyle \mathcal{B}$ is a basis for S ⇔ ∀ B ∈ $\displaystyle \mathcal{B}_p$ : B is an open neighborhood of p (in S) ∧ ∀ open set U (in S) : ∃ $\displaystyle \text{B}_i$ ... ⊂ $\displaystyle \mathcal{B}$ such that U = $\displaystyle \bigcup_{\displaystyle i \isin \text{I}} \text{B}_i$ )  
// every open set (in S) is a union of sets from $\displaystyle \mathcal{B}$  

\[Theorem\] Union of Local Bases is Basis 局部基的并集是基  
\- \[Tu 2011\] / Proposition A.7  
\- ProofWiki / Union of Local Bases is Basis  
S is topological space ⇒ ( $\displaystyle \mathcal{B}_p$ is a local basis at p (in S) ∧ $\displaystyle \mathcal{B}$ = $\displaystyle \bigcup_{\displaystyle p \isin \text{S}} \mathcal{B}_p$ ⇒ $\displaystyle \mathcal{B}$ is a basis for S )  

> proof  
to prove "$\displaystyle \mathcal{B}$ is a basis for S", it suffices to prove "∀ open set U in S : ∃ $\displaystyle \text{B}_i$ ... ∈ $\displaystyle \mathcal{B}$ such that U = $\displaystyle \bigcup_{\displaystyle i \isin \text{I}} \text{B}_i$"  
by "Definition of Local Basis", p ∈ U ⇒ (let $\displaystyle \mathcal{B}_p$ be the local basis at p) ∃ $\displaystyle \text{B}_p$ ∈ $\displaystyle \mathcal{B}_p$ ⊂ $\displaystyle \mathcal{B}$ such that p ∈ $\displaystyle \text{B}_p$ ⊂ U ⇒ U = $\displaystyle \bigcup_{\displaystyle p \isin \text{U}} \text{B}_p$  
  
\[Theorem\] Basis induces Local Basis 基诱导局部基  
\- \[Tu 2011\] / Proposition A.7  
\- ProofWiki / Basis induces Local Basis  
S is topological space ⇒ ( $\displaystyle \mathcal{B}$ is a basis for S ∧ $\displaystyle \mathcal{B}_p$ = { $\displaystyle \text{B}_p$ : p ∈ $\displaystyle \text{B}_p$ ∧ $\displaystyle \text{B}_p$ ∈ $\displaystyle \mathcal{B}$ } ⇒ $\displaystyle \mathcal{B}_p$ is a local basis at p (in S) )  

> proof  
to prove "$\displaystyle \mathcal{B}_p$ is a local basis at p (in S)", it suffices to prove "∀ open neighborhood U of p (in S) : ∃ $\displaystyle \text{B}_p$ ∈ $\displaystyle \mathcal{B}_p$ such that $\displaystyle \text{B}_p$ ⊂ U"  
by "Definition of Basis", open neighborhood U of p (in S) ⇒ ∃ $\displaystyle \text{B}_i$ ... ∈ $\displaystyle \mathcal{B}$ such that U = $\displaystyle \bigcup_{\displaystyle i \isin \text{I}} \text{B}_i$ ⇒ (since p ∈ U) ∃ i ∈ I such that p ∈ $\displaystyle \text{B}_i$ ⇒ (since p ∈ $\displaystyle \text{B}_i$ ∧ $\displaystyle \text{B}_i$ ∈ $\displaystyle \mathcal{B}$) $\displaystyle \text{B}_i$ ∈ $\displaystyle \mathcal{B}_p$ ⇒ ∃ $\displaystyle \text{B}_i$ ∈ $\displaystyle \mathcal{B}_p$ such that $\displaystyle \text{B}_i$ ⊂ U 

\[Theorem\] Synthetic Basis and Analytic Basis are Compatible 综合基和分析基兼容  
\- \[Tu 2011\] / Proposition A.8  
\- ProofWiki / Definition:Basis (Topology)/Synthetic Basis  
\- ProofWiki / Synthetic Basis and Analytic Basis are Compatible  
S is topological space ⇒ ( $\displaystyle \mathcal{B}$ is a basis for S ⇔ $\displaystyle \mathcal{B}$ ⊂ $\displaystyle \wp ( \text{S} )$ ∧ ∃ $\displaystyle \text{B}_i$ ... ∈ $\displaystyle \mathcal{B}$ such that S = $\displaystyle \bigcup_{\displaystyle i \isin \text{I}} \text{B}_i$ ∧ ∀ U V ∈ $\displaystyle \mathcal{B}$ : ∃ $\displaystyle \text{B}_i$ ... ∈ $\displaystyle \mathcal{B}$ such that U ∩ V = $\displaystyle \bigcup_{\displaystyle i \isin \text{I}} \text{B}_i$ )  
> proof  
TODO  

\[Theorem\] Basis for Topological Subspace 拓扑子空间的基  
\- \[Tu 2011\] / Proposition A.9  
\- ProofWiki / Basis for Topological Subspace  
S is topological space ∧ A is a topological subspace of S ⇒ ( $\displaystyle \mathcal{B}$ is a basis for S ∧ $\displaystyle \mathcal{B}_A$ = { B ∩ A : B ∈ $\displaystyle \mathcal{B}$ } ⇒ $\displaystyle \mathcal{B}_A$ is a basis for A )  
   
> proof  
open neighborhood $\displaystyle \text{U}_A$ of p in A ⇒ ∃ open neighborhood U of p in S such that $\displaystyle \text{U}_A$ = U ∩ A  ⇒ (since p ∈ U ∩ A  ⊂ U) p ∈ U ⇒ ∃ $\displaystyle \text{B}_p$ ∈ $\displaystyle \mathcal{B}_p$ ⊂ $\displaystyle \mathcal{B}$ such that p ∈ $\displaystyle \text{B}_p$ ⊂ U ⇒ p ∈ $\displaystyle \text{B}_p$ ∩ A ⊂ U ∩ A = $\displaystyle \text{U}_A$ ⇒ ∃ $\displaystyle {\text{B}_A}_p$ = $\displaystyle \text{B}_p$ ∩ A such that p ∈ $\displaystyle {\text{B}_A}_p$ ⊂ $\displaystyle \mathcal{B}_A$  

---      

第二可数   
//\[Browder 1996\] / 6.27 Definition           

---    

ProofWiKi / Metric Space is First-Countable    

ProofWiki / Countable Basis of Real Number Line   

### 分离公理 Separation Axiom          
              
\[定义\]Hausdorff(豪斯多夫)空间 //分离空间 Separated Space //T2空间 //T -> Tychonoff 吉洪诺夫 //分离公理 Separation Axiom                  
X是拓扑空间 ⇒ ( X是豪斯多夫空间 ⇔ ( ∀ x,y ∈ X : x≠y ⇒ ( ∃ $\displaystyle \text{U}_x$,$\displaystyle \text{V}_y$,$\displaystyle \text{U}_x$是x的(在X上的)开领域,$\displaystyle \text{V}_y$是y的(在X上的)开领域 : $\displaystyle \text{U}_x$ ∩ $\displaystyle \text{V}_y$ = ∅ ) ) )           
//ProofWiki / Definition:Hausdorff Space          
//\[陈天权 2009\] / 定义 7\.5\.2     
         
---    
    
\[定理\] Hausdorff(豪斯多夫)空间的子集 ⇒ (紧的 ⇒ 闭集)            
X是拓扑空间 且 X是Hausdorff(豪斯多夫)空间 且 Y ⊂ X ⇒ ( Y是紧的 ⇒ Y是闭集 )              
//ProofWiki / Compact Subspace of Hausdorff Space is Closed          
//\[陈天权 2009\] / 命题 7\.6\.4       
> 证明                      
> 对任意p ∈ (X − Y)，我们有           
>                  
> 对任意q ∈ Y，由于p ∈ (X − Y) $\displaystyle \notin$ Y，显然有p≠q，又因为X是Hausdorff(豪斯多夫)空间，从而 存在p的开领域$\displaystyle \text{U}_p$和q的开领域$\displaystyle \text{V}_q$ 满足$\displaystyle \text{U}_p$ ∩ $\displaystyle \text{V}_q$ = ∅       
> 显然，以上的开领域$\displaystyle \text{V}_q$构成的集合{ $\displaystyle \text{V}_q$ | q ∈ Y } 是Y的一个开覆盖，由于Y是紧的，因此存在关于Y的有限子覆盖，即可以从开覆盖中选择有限个开集$\displaystyle \text{V}_q$来覆盖Y                       
> 将以上有限个开领域$\displaystyle \text{V}_q$对应的有限个开领域$\displaystyle \text{U}_p$的交记作F，即F = $\displaystyle \bigcap \text{U}_p$，根据拓扑的定义，F为开集  //根据拓扑的定义 开集只对**有限**交封闭 因此需要先证明**有限** 才能证明F为开集                                 
> 显然，有$\displaystyle \bigcap \text{U}_p$ ∩ $\displaystyle \bigcup \text{V}_q$ = ∅，又由于将以上有限个开领域$\displaystyle \text{V}_q$是Y的覆盖，有Y ⊂ $\displaystyle \bigcup \text{V}_q$  从而有$\displaystyle \bigcap \text{U}_p$ ∩ Y = ∅，即$\displaystyle \bigcap \text{U}_p$ ⊂ (X − Y)       
>                         
> 从而，我们有 ∀ p ∈ (X − Y) : ∃ F = $\displaystyle \bigcap \text{U}_p$ : F是p的开领域 且 F ⊂ (X − Y)                
>                 
> 即 ∀ p ∈ (X − Y) : p是(X − Y)的内点 //根据内点的定义    
> 从而有 (X − Y)是开集 //根据"\[定理\] \[等价定义\] 开集(Open Set) //通过 内点(Interior Point)"            
> 从而Y是闭集合 //根据闭集的定义  
>     

---      

\[定理\] Hausdorff(豪斯多夫)空间 ⇒ 极限的唯一性 //Uniqueness of the limit           
X是拓扑空间 且 X是Hausdorff(豪斯多夫)空间 ⇒ ( $\displaystyle {\lang x_n \rang}_{ n \isin \N }$是X上的无限序列 且 $\displaystyle {\lang x_n \rang}_{ n \isin \N }$(在X上)收敛于a 且 $\displaystyle {\lang y_n \rang}_{ n \isin \N }$是X上的无限序列 且 $\displaystyle {\lang y_n \rang}_{ n \isin \N }$(在X上)收敛于b ⇒ a = b )    
//ProofWiki / Convergent Sequence in Hausdorff Space has Unique Limit    
//\[Tu 2011\] / Definition A.55   
//注意：由于"Y ⊂ X 且 $\displaystyle {\lang x_n \rang}_{ n \isin \N }$是Y上的无限序列 ⇒ $\displaystyle {\lang x_n \rang}_{ n \isin \N }$是X上的无限序列"，因此X的子集上的无限序列仍适用于本定理       
//注意：Hausdorff(豪斯多夫)空间并不是极限点唯一性成立的必要条件 //ProofWiki / Space in which All Convergent Sequences have Unique Limit not necessarily Hausdorff    
> 证明          
> 反证法，假设命题不成立，即有a≠b成立        
> 因为X是Hausdorff(豪斯多夫)空间，存在x的开领域$\displaystyle \text{U}_x$和y的开领域$\displaystyle \text{V}_y$ 满足$\displaystyle \text{U}_a$ ∩ $\displaystyle \text{V}_b$ = ∅       
> 根据拓扑空间中序列收敛的定义，∀$\displaystyle \text{U}_a$ : $\displaystyle \text{U}_a$是a的(在X上的)开领域 ⇒ ( ∃ $\displaystyle \text{N}_a$ > 0 : ∀ n > $\displaystyle \text{N}_a$ : $\displaystyle x_n$ ∈ $\displaystyle \text{U}_a$ ) 并且 ∀$\displaystyle \text{V}_b$ : $\displaystyle \text{V}_b$是b的(在X上的)开领域 ⇒ ( ∃ $\displaystyle \text{N}_b$ > 0 : ∀ n > $\displaystyle \text{N}_b$ : $\displaystyle x_n$ ∈ $\displaystyle \text{V}_b$ )         
> 从而 ∀$\displaystyle \text{U}_a$,$\displaystyle \text{V}_b$ : $\displaystyle \text{U}_a$是a的(在X上的)开领域 且 $\displaystyle \text{V}_b$是b的(在X上的)开领域 ⇒ ( ( 取N = max\{ $\displaystyle \text{N}_a$, $\displaystyle \text{N}_b$ \} 有∀ n > N : $\displaystyle x_n$ ∈ $\displaystyle \text{U}_a$ 且 $\displaystyle x_n$ ∈ $\displaystyle \text{V}_b$ ) ⇒ ( $\displaystyle \text{U}_a$ ∩ $\displaystyle \text{V}_b$ ≠ ∅ ) ) 与 "存在x的开领域$\displaystyle \text{U}_x$和y的开领域$\displaystyle \text{V}_y$ 满足$\displaystyle \text{U}_a$ ∩ $\displaystyle \text{V}_b$ = ∅" 矛盾        
>              

### 积空间 Product Topology
\- ProofWiki / Definition:Product Space (Topology)  
\- ProofWiki / Definition:Product Topology          
\- \[Tu 2011\] / A.6 Product Topology  


### Continuity //连续性  
\- \[Tu 2011\] / A.7 Continuity      

#### Continuous Mapping (Topology) //连续映射(拓扑)  
\- ProofWiki / Definition:Continuous Mapping (Topology)     
                    
#### Continuous at a Point //在点处连续  
\- ProofWiki / Definition:Continuous Mapping (Topology)/Point  
\- ProofWiki / Equivalence of Definitions of Continuous Mapping between Topological Spaces     

\[Definition\] Definition:Continuous Mapping (Topology)/Point / Definition using Neighborhoods   
\- \[Tu 2011\] / A.7 Continuity      
\- \[陈天权 2009\] / 定义 7\.2\.1  
X is topological space ∧ Y is topological space ⇒ ( mapping f: X → Y is continuous at p ⇔ ∀ neighborhood V of f(p) in Y : ∃ neighborhood U of p in X such that f(U) ⊂ V )  

//对R的通常拓扑，间断点处只能找到半开半闭区间，不属于领域　　   

#### Continuous on a Set //在集合上连续    
\- ProofWiki / Definition:Continuous Mapping (Topology)/Set

\[Definition\] Definition:Continuous Mapping (Topology)/Set   
\- \[Tu 2011\] / A.7 Continuity      
\- \[陈天权 2009\] / 定义 7\.2\.1  
X is topological space ∧ Y is topological space ∧ A ⊂ X ⇒ ( mapping f: X → Y is continuous on A ⇔ ∀ p ∈ A : f is continuous at p )  

\[Theorem\] Continuous iff inverse image of any open set is open //连续 等价于 开集的逆像是开集  
\- ProofWiki / Continuous iff inverse image of any open set is open  
\- ProofWiki / Image of Interval by Continuous Function is Interval  
\- \[Tu 2011\] / Proposition A.23 (Continuity in terms of open sets)  
\- [陈天权 2009\] / 命题 7\.2\.1   
X is topological space ∧ Y is topological space ⇒ ( mapping f: X → Y is continuous on X ⇔ ∀ open set V in Y : inverse image $\displaystyle \operatorname{f^{-1}}$(V) is an open set in X )  

> proof  
>  
> necessity  
by "Definition of Continuous Mapping", we have that "p ∈ $\displaystyle \operatorname{f^{-1}}$(V) ⇒ f(p) ∈ V ⇒ ∃ neighborhood U of p in X such that f(U) ⊂ V ⇒ p is a interior point of $\displaystyle \operatorname{f^{-1}}$(V)". // f(U) ⊂ V implies U ⊂ $\displaystyle \operatorname{f^{-1}}$(V) // $\displaystyle \operatorname{f^{-1}}$(V)是X的子集中可能满足对应的像包含于V的最大的集合   
since "**every point of $\displaystyle \operatorname{f^{-1}}$(V) is an interior point**", we have that "$\displaystyle \operatorname{f^{-1}}$(V) is an open set".  
> 
> sufficiency  
to prove "f is continuous on X", it suffices to prove "∀ p ∈ X : f is continuous at p"  
neighborhood V of f(p) in Y ⇒ ∃ open set $\displaystyle \text{V}_1$ such that f(p) ⊂ $\displaystyle \text{V}_1$ ⊂ V ⇒ $\displaystyle \operatorname{f^{-1}} ( \text{V}_1 )$ is an open set in X ⇒ ∃ neighborhood $\displaystyle \operatorname{f^{-1}} ( \text{V}_1 )$ of p in X such that f($\displaystyle \operatorname{f^{-1}} ( \text{V}_1 )$) ⊂ V // f(p) ⊂ $\displaystyle \text{V}_1$ implies that p ∈ $\displaystyle \operatorname{f^{-1}} ( \text{V}_1 )$ // $\displaystyle \text{V}_1$ ⊂ V implies that f($\displaystyle \operatorname{f^{-1}} ( \text{V}_1 )$) = $\displaystyle \text{V}_1$ ⊂ V   
                
### 度量 Metric                  
      
\[定义\] 度量空间(Metric Space)     
ProofWiki / Definition:Metric Space     
(X,ρ)是度量空间 ⇔ X ≠ ∅ 且 ρ是X×X到R的映射 且 ρ满足度量空间公理    
度量空间公理(Metric Space Axioms)

ρ是X×X到R的映射 ⇒ ( ρ满足度量空间公理 ⇔ ρ(x,y) = 0 ⇔ x = y /\* 不可分的同一性 \*/ 且 ρ(x,y) = ρ(y,x) /\* 对称性 \*/ 且 ρ(x,z) ≤ ρ(x,y) + ρ(y,z) /\* 次可加性/三角不等式 \*/ )                      
不可分的同一性(Identity of Indiscernibles)  
对称性(Symmetric)   
次可加性(Subadditivity)/三角不等式(Triangle Inequality)     
//\[陈天权 2009\] / 定义 7\.3\.1       
              
(X,ρ)是度量空间 ⇒ ρ是距离函数/度量         
距离函数(Distance Function)       
度量(Metric)     
            
---           
           
\[定义\] 开球(Open Ball)             
(X,ρ)是度量空间 且 a ∈ X 且 ε > 0 ⇒ ( B(a,ε)是以a为球心以ε为半径的开球 ⇔ B(a,ε) = \{ x ∈ X | ρ(x,a) < ε \} )     
ProofWiki / Definition:Open Ball      
球心(Center)      
半径(Radius)     
        
\[定义\] 开集(Open Set) //度量空间(Metric Space)      
(X,ρ)是度量空间 ⇒ ( U是((X,ρ)上的)开集 ⇔ ∀"x ∈ U","∃"ϵ > 0","B(a,ε) ⊂ U"" )    
ProofWiki / Definition:Open Set/Metric Space        
//可以从"\[定理\] \[等价定义\] 开集(Open Set) //通过 内点(Interior Point)"的角度理解    
      
\[定义\] 度量诱导的拓扑(Topology Induced by Metric) / 度量拓扑(Metric Topology) //拓扑是度量的弱化 没有距离的概念 只有(开)领域的概念       
(X,ρ)是度量空间 ⇒ ( τ是ρ上的度量拓扑 ⇔ τ是(X,ρ)诱导的拓扑 ⇔ τ = \{ U | U是((X,ρ)上的)开集 \} )        
ProofWiki / Definition:Topology Induced by Metric   
//根据拓扑的定义可以证明，(X,ρ)是度量空间 ⇒ ( τ是(X,ρ)诱导的拓扑 ⇒ τ是X上的拓扑 )     
//\[陈天权 2009\] / 命题 7\.3\.1       
//\[陈天权 2009\] / 定义 7\.3\.3       
       
引入基(Basis)的概念          
//\[陈天权 2009\] / 定义 7\.4\.2        
//\[陈天权 2009\] / 例 7\.4\.2        
           
---     
    
度量子空间(Subspace)    
//ProofWiki / Definition:Metric Subspace    
//\[陈天权 2009\] / 定义 7\.4\.1    

---   

\[定义\] 有界的(Bounded)   
(X,ρ)是度量空间 且 Y ⊂ X ⇒ ( Y是有界的 ⇔ ∃"ϵ > 0","∀"x,y ∈ Y","ρ(x,y) < ϵ"" )           
//ProofWiki / Definition:Bounded Metric Space      
//\[Browder 1996\] / 6.60 Definition                 
//\[陈天权 2009\] / 定义 7\.6\.3    
       
\[定义\] 网(Net)     
(X,ρ)是度量空间 且 Y ⊂ X 且 S ⊂ X ⇒ ( S是Y的ϵ-网 ⇔ ϵ > 0 且 Y ⊂ $\displaystyle \bigcup_{x \isin \text{S}} \operatorname{B}( x , \varepsilon )$ )      
//ProofWiki / Definition:Net (Metric Space)      
//\[陈天权 2009\] / 定义 7\.6\.4       

\[定义\] 有限网(Finite Net)   
(X,ρ)是度量空间 且 Y ⊂ X ⇒ ( S是Y的有限ϵ-网 ⇔ S是Y的ϵ-网 且 S是有限集 )        
//ProofWiki / Definition:Net (Metric Space)/Finite Net        
//\[陈天权 2009\] / 定义 7\.6\.4       

\[定义\] 全有界的(Totally Bounded)        
(X,ρ)是度量空间 且 Y ⊂ X ⇒ ( Y是全有界的 ⇔ ∀"ϵ > 0","∃"S ⊂ X","S是Y的有限ϵ-网"" )      
//ProofWiki / Definition:Totally Bounded Metric Space     
//\[Browder 1996\] / 6.61 Definition                 
//\[陈天权 2009\] / 定义 7\.6\.4       

\[定理\] 全有界的(Totally Bounded) ⇒ 有界的(Bounded)    
//ProofWiki / Totally Bounded Metric Space is Bounded
     
---    
     
\[定理\] 度量空间 ⇒ Hausdorff(豪斯多夫)空间      
(X,ρ)是度量空间 且 (X,τ)是(X,ρ)诱导的拓扑空间 ⇒ (X,τ)是Hausdorff(豪斯多夫)空间    
ProofWiki / Metric Space is Hausdorff  
> 证明     
> 设有x,y ∈ X 且 x≠y       
> 根据"不可分的同一性"，有d(x,y)≠0     
> 将z=x应用到"次可加性"，有d(x,x) ≤ d(x,y) + d(y,x)，从而 0/\* 不可分的同一性 \*/ = d(x,x) ≤ d(x,y) + d(x,y)/\* 对称性 \*/ 即 0 ≤ 2 ⋅ d(x,y) 即 d(y,x) ≥ 0            
> 从而有d(x,y)>0，取ε = $\displaystyle \frac{\operatorname{d}(x,y)}{2}$ /\*证明时，可以较随意地选取该值，比如$\displaystyle \frac{\operatorname{d}(x,y)}{3}$，$\displaystyle \frac{\operatorname{d}(x,y)}{4}$均可\*/，有B(x,ε) ∩ B(y,ε) = ∅ //可以用反证法证明，假设存在p ∈ B(x,ε) ∩ B(y,ε)，那么，根据开球的定义，有d(p,x) + d(p,y) < ε + ε = d(x,y)，与次可加性矛盾    
>                   

\[定理\] \[等价定义\] 收敛序列(Convergent Sequence) //度量空间中的序列极限 //严格意义上应当由拓扑空间中的序列极限推出          
         


---     

\[定义\] Cauchy(柯西)序列(Sequence) //度量空间中的Cauchy(柯西)序列                  
(X,ρ)是度量空间 且 Y ⊂ X 且 $\displaystyle {\lang x_n \rang}_{ n \isin \N }$是Y上的无限序列 ⇒ ( $\displaystyle {\lang x_n \rang}_{ n \isin \N }$是(X上的)Cauchy(柯西)序列 ⇔ ( ∀ ε > 0 : ∃ N > 0 : ∀ m,n > N : ρ($\displaystyle x_m$, $\displaystyle x_n$) < ε ) )     
//ProofWiki / Definition:Cauchy Sequence/Metric Space         
//\[陈天权 2009\] / 定义 7\.5\.3    
            
---     

\[定理\] 收敛序列 ⇒ Cauchy(柯西)序列           
//ProofWiki / Convergent Sequence is Cauchy Sequence/Metric Space             
             
            
---          

\[定理\] Cauchy(柯西)序列 ⇒ ( 存在子列/\* 列紧 \*/收敛于a ⇒ Cauchy(柯西)序列收敛于a )            
(X,ρ)是度量空间 ⇒ ( $\displaystyle {\lang x_n \rang}_{ n \isin \N }$是X上的Cauchy(柯西)序列 ⇒ ( ∃ $\displaystyle {\lang x_{n_k} \rang}_{ k \isin \N }$是$\displaystyle {\lang x_n \rang}_{ n \isin \N }$的子列 : ∃ a ∈ X : $\displaystyle {\lang x_{n_k} \rang}_{ k \isin \N }$在X上收敛于a ⇒ $\displaystyle {\lang x_n \rang}_{ n \isin \N }$在X上收敛于a )             
//ProofWiki / Convergent Subsequence of Cauchy Sequence/Metric Space       
//注意：由于"Y ⊂ X 且 $\displaystyle {\lang x_n \rang}_{ n \isin \N }$是Y上的无限序列 ⇒ $\displaystyle {\lang x_n \rang}_{ n \isin \N }$是X上的无限序列"，因此X的子集上的无限序列仍适用于本定理                         
//\[陈天权 2009\] / 引理 7\.6\.1       
> 证明     
> ∀ ε > 0 :      
> 由于$\displaystyle {\lang x_n \rang}_{ n \isin \N }$是X上的Cauchy(柯西)序列，对于$\displaystyle \frac{\varepsilon}{2}$ /\*证明时，可以较随意地选取该值，比如$\displaystyle \frac{\varepsilon}{3}$，$\displaystyle \frac{\varepsilon}{4}$均可\*/ 有 ∃ N > 0 : ∀ m,n > N : ρ($\displaystyle x_m$, $\displaystyle x_n$) < $\displaystyle \frac{\varepsilon}{2}$     
> 由于$\displaystyle {\lang x_{n_k} \rang}_{ k \isin \N }$在X上收敛于a，对于$\displaystyle \frac{\varepsilon}{2}$ 有 ∃ K > 0 : ∀ k > K : ρ($\displaystyle x_{n_k}$, a) < $\displaystyle \frac{\varepsilon}{2}$     
> 显然，存在$\displaystyle k_1$ > K 满足$\displaystyle n_{k_1}$ > N /\* 一说基于阿基米德原理 \*/，有 ρ($\displaystyle x_{n_{k_1}}$, a) < $\displaystyle \frac{\varepsilon}{2}$ 且 ∀ n > N : ρ($\displaystyle x_{n_{k_1}}$, $\displaystyle x_n$) < $\displaystyle \frac{\varepsilon}{2}$          
>      
> 从而有 ∀ ε > 0 : ∃ N > 0 : ∀ n > N : $\displaystyle x_n+$ ≤ ρ($\displaystyle x_{n_{k_1}}$, a) + ρ($\displaystyle x_{n_{k_1}}$, $\displaystyle x_n$) < $\displaystyle \frac{\varepsilon}{2}$ + $\displaystyle \frac{\varepsilon}{2}$ < ε，根据收敛序列的定义，命题得证             
>      
       
---          
           
\[定义\] 完备的(Complete) //度量空间(Metric Space)         
(X,ρ)是度量空间 ⇒ ( (X,ρ)是完备的 ⇔ ( ∀ $\displaystyle {\lang x_n \rang}_{ n \isin \N }$是X上的无限序列 : $\displaystyle {\lang x_n \rang}_{ n \isin \N }$是(X上的)Cauchy(柯西)序列 ⇒ ∃ a : $\displaystyle {\lang x_n \rang}_{ n \isin \N }$(在X上)收敛于a ) )       
//ProofWiki / Definition:Complete Metric Space      
//\[陈天权 2009\] / 定义 7\.6\.5       
注意：逆命题"收敛序列 ⇒ Cauchy(柯西)序列"是一定成立的 /\* \[定理\] 收敛序列 ⇒ Cauchy(柯西)序列 \*/，完备集也相当于两者等价，即"Cauchy(柯西)序列 ⇔ 收敛序列"                      
             
                
\[定理\] 完备(Complete)度量空间的子空间(Subspace) ⇒ ( 完备(Complete) ⇔ 闭集(Closed) ) //完备度量空间的子空间并不一定完备 //与紧空间不同               
(X,ρ)是度量空间 且 (X,ρ)是完备的 且 (Y,ρ)是(X,ρ)的度量子空间 ⇒ ( (Y,ρ)是完备的 ⇔ (Y,ρ)是闭集 )                                   
//ProofWiki / Subspace of Complete Metric Space is Closed iff Complete   
//\[陈天权 2009\] / 命题 7\.5\.4       
> 证明     
> 显然，根据Cauchy(柯西)序列的定义，有 ∀ $\displaystyle {\lang x_n \rang}_{ n \isin \N }$是Y上的无限序列 : $\displaystyle {\lang x_n \rang}_{ n \isin \N }$是(Y上的)Cauchy(柯西)序列 ⇒ $\displaystyle {\lang x_n \rang}_{ n \isin \N }$是(X上的)Cauchy(柯西)序列                  
> 又由于X是完备的，有 $\displaystyle {\lang x_n \rang}_{ n \isin \N }$是(X上的)Cauchy(柯西)序列 ⇒  ∃ a : $\displaystyle {\lang x_n \rang}_{ n \isin \N }$(在X上)收敛于a           
> 根据完备集的定义，要证明Y是完备的，相当于证明 ∀ $\displaystyle {\lang x_n \rang}_{ n \isin \N }$是Y上的无限序列 : ∃ a : $\displaystyle {\lang x_n \rang}_{ n \isin \N }$(在X上)收敛于a ⇒ ∃ b : $\displaystyle {\lang x_n \rang}_{ n \isin \N }$(在Y上)收敛于b          
> 相当于证明 ∀ $\displaystyle {\lang x_n \rang}_{ n \isin \N }$是Y上的无限序列 : ∃ a : $\displaystyle {\lang x_n \rang}_{ n \isin \N }$(在X上)收敛于a ⇒ a ∈ Y //假设存在b满足序列在Y上收敛于b，那么显然有序列在X上收敛于b，又由于极限点的唯一性，一定有b=a；也就是说，可以认为在Y内满足"∀$\displaystyle \text{U}_a$ : $\displaystyle \text{U}_a$是a的(在Y上的)开领域 ⇒ ( ∃ N > 0 : ∀ n > N : $\displaystyle x_n$ ∈ $\displaystyle \text{U}_a$ )"的点只有a，然而，根据拓扑空间中序列收敛的定义，还需要满足a ∈ Y，从而命题等价于证明a ∈ Y          
> 根据 "\[定理\] (序列的)极(限)点 ⇒ 附着点（即在闭包内）"，Y = Y的闭包，从而Y是闭集    
>                          
    
---      

Picard 关于微分方程的定理     

---     

\[定理\] 紧 ⇒ 列紧 //度量空间诱导的拓扑空间           
(X,ρ)是度量空间 且 (X,τ)是(X,ρ)诱导的拓扑空间 ⇒ ( X(在X上)是紧的 ⇒  X(在X上)是列紧的 )  
//ProofWiki / Compact Subspace of Metric Space is Sequentially Compact in Itself   
//\[陈天权 2009\] / 定理 7\.6\.3     
//注：该定理存在更泛化的版本 ProofWiki / Countably Compact First-Countable Space is Sequentially Compact //拓扑空间适用，不要求度量空间                    

---          

海涅-博雷尔定理 Heine–Borel Theorem //在度量(Metric)空间上                      
Compact iff Complete and Totally Bounded 
    
---      
    
斯通-魏尔施特拉斯定理 Stone-Weierstrass Theorem       

---    

### Euclidean(欧几里得)              
     
    
---   

\[定理\] Euclidean(欧几里得)空间的子空间 ⇒ ( 完备的(Complete) ⇔ 闭集(Closed) )              

//ProofWiki / Real Number Line is Complete Metric Space    
//ProofWiki / Euclidean Space is Complete Metric Space    
//\[Browder 1996\] / 6.60 Definition       
//\[Browder 1996\] / 6.61 Proposition                 
        
---     
     
\[定理\] Euclidean(欧几里得)空间的子空间 ⇒ ( 全有界的(Totally Bounded) ⇔ 有界的(Bounded) )             

//ProofWiki / Bounded Subspace of Euclidean Space is Totally Bounded    
//ProofWiki / Totally Bounded Metric Space is Bounded    
//\[Browder 1996\] / 6.62 Proposition                 
     
      
     
---    

海涅-博雷尔定理 Heine–Borel Theorem //在Euclidean(欧几里得)空间上              
//\[Browder 1996\] / 6.64 Corollary                 


---   

有限覆盖定理 //海涅-博雷尔定理 Heine–Borel Theorem //在R上             
\[定理\] R ⇒ ( 有界闭集 ⇒ 紧的 )        
//ProofWiki / Closed Bounded Subset of Real Numbers is Compact     
//ProofWiki / Compact Subspace of Real Numbers is Closed and Bounded    
//\[Browder 1996\] / 6.49 Theorem     
//\[Browder 1996\] / 6.53 Corollary            
                                      
---              

欧几里得空间 Euclidean Space      
$\displaystyle R^k$上的欧几里得空间 度量 d(x,y) = |x - y| //度量被定义为向量的模     

---    

拓扑间的包含关系     
//finer/smaller/weaker    
//coarser/larger/stronger  

---    
        
平凡拓扑 Trivial Topology     
离散拓扑 Discrete Topology   
    
//显然，对于任意集合X：  
//{∅, X}是X上的拓扑 被称为平凡拓扑 //\[陈天权 2009\] / 例 7\.1\.2         
//$\wp(X)$是X上的拓扑 被称为离散拓扑 //\[陈天权 2009\] / 例 7\.1\.1     
        
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
    
###    
    

---    
     


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

---  


         
R上的闭区间是（关于R的通常拓扑的）紧集   
\[陈天权 2009\] / 例 7\.6\.1       

根据 有限覆盖定理 即可证明

                                                       
          
        
---                
          
斯通-魏尔施特拉斯逼近定理 / Stone-Weierstrass Theorem      
//\[陈天权 2009\] / 定理 7\.7\.2         
//\[Rudin 1976\] / 7\.32 Theorem       


### 参考文献  
\[Tu 2011\] Loring Tu. "An Introduction to Manifolds, Second Edition." Springer 2011.  
\[陈天权 2009\] 陈天权. "数学分析讲义." 北京大学出版社 2009.    
\[同济大学数学系 2014\] 同济大学数学系. "高等数学 第七版." 高等教育出版社 2014.   
\[Browder 1996\] Andrew Browder. "Mathmatical Analysis, An Introduction." Springer 1996.   
\[Yeh 2014\] James Yeh. "Real Analysis: Theory of Measure and Integration, Third Edition." World Scientific 2014
 