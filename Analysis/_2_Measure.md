## License  
```  
Copyright (C) YuqiaoZhang

This program is free software: you can redistribute it and/or modify it under the terms of the GNU Lesser General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU Lesser General Public License for more details.

You should have received a copy of the GNU Lesser General Public License along with this program.  If not, see <https://www.gnu.org/licenses/>
```  

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
> 显然，由于$\displaystyle \bigcup_{n \isin \N} B_n$ ⊂ $\displaystyle \bigcup_{n \isin \N} B_n$，取 A=$\displaystyle \bigcup_{n \isin \N} B_n$, 有\"μ($\displaystyle \bigcup_{n \isin \N} B_n$) ≤ $\displaystyle \sum_{n \isin \N}$μ($\displaystyle B_n$)\"   
>     
> 1 ⇒ 2   
>  ∀\"集合A,B ∈ ℘(X) 满足 A ⊂ $\displaystyle \bigcup_{n \isin \N} B_n$\"，有\"    
> μ(A) ≤ μ($\displaystyle \bigcup_{n \isin \N} B_n$) //∀\"集合A,B ∈ ℘(X) 满足 A ⊂ B\"          
> μ($\displaystyle \bigcup_{n \isin \N} B_n$) ≤ $\displaystyle \sum_{n \isin \N}$μ($\displaystyle B_n$) //∀\"集合$\displaystyle B_1$,$\displaystyle B_2$,... ∈ $\displaystyle \mathcal{R}$\"      
> 即 μ(A) ≤ μ($\displaystyle \bigcup_{n \isin \N} B_n$) ≤ $\displaystyle \sum_{n \isin \N}$μ($\displaystyle B_n$)    
> \"        
>     
     
覆盖  
//覆盖的定义并不依赖于拓扑   
//见紧空间  
C = { $\displaystyle \text{U}_\alpha$ | α ∈ A } ⇒ ( C是Y的覆盖 ⇔ Y ⊂ $\displaystyle \bigcup_{\alpha \isin \text{A}} \text{U}_\alpha$ )    
//本质上来讲，定义中的指标集(Index Set)可以忽略， 理解为"Y 包含于 C中所有的元素的并集"即可 //即Y ⊂ $\displaystyle \bigcup_{\text{U} \isin \text{C}}$U    

构造外测度 //Construction of Outer Measure       
Y ⊂ ℘(X) 且 ∅ ∈ Y 且 p是Y到非负扩展实数集(\[0,+∞\])的映射 且 p(∅)=0 且 φ的定义域为 ℘(X) 且 φ(E) = $\displaystyle \begin{cases} \displaystyle \inf \{ \sum_{A \isin \text{C}} \operatorname{p} ( A ) \, | \, \text{C} \text{是} \text{可数集} \, \text{且} \, \text{C} \text{是} E \text{的覆盖} \, \text{且} \text{C} \subset Y \} & \displaystyle \text{当} \, \exist \text{"} \text{C} \text{","} \text{C} \text{是} \text{可数集} \, \text{且} \, \text{C} \text{是} E \text{的覆盖} \, \text{且} \, \text{C} \subset Y \text{"} \, \text{时} \\ +\infty & \displaystyle \text{当} \, \nexists \text{"} \text{C} \text{","} \text{C} \text{是} \text{可数集} \, \text{且} \, \text{C} \text{是} E \text{的覆盖} \, \text{且} \, \text{C} \subset Y \text{"} \, \text{时} \end{cases}$ ⇒ φ是X上的外测度     
//关于φ(E)，可以理解为 所有可能的"包含于Y且覆盖E的可数集C" "C中的所有的元素在P中的像的累加"   
\[Rudin 1976\] / 11.7 Definition    
\[陈天权 2009\] / 引理 9.3.1    

证明 
> 
> 由于 p(∅)=0 且 p非负，显然 φ(∅)=0  
> 
> ∀ \"集合A,B ∈ ℘(X) 满足 A ⊂ B\"，有\"显然 { $\displaystyle \sum_{D \isin C}$p(D) | C是可数集 且 C是A的覆盖 且 C ⊂ Y } ⊂ { $\displaystyle \sum_{D \isin C}$p(D) | C是可数集 且 C是B的覆盖 且 C ⊂ Y }     
> 根据下确界的定义，显然 φ(A) ≤ φ(B)\"
>       
> ---      
>      
> ∀ \"集合$\displaystyle S_1$,$\displaystyle S_2$,... ∈ ℘(X)\"，有\" 如果 ∃ \' n ∈ $\displaystyle \N$ \'，满足 \' ∄ C是可数集 且 C是$\displaystyle S_n$的覆盖 且 C ⊂ Y \'，那么 ∄ C是可数集 且 C是$\displaystyle \bigcup_{i \isin \N} S_i$的覆盖 且 C ⊂ Y，从而 φ($\displaystyle S_n$)=+∞ 且 φ($\displaystyle \bigcup_{i \isin \N} S_i$)=+∞，从而 φ($\displaystyle \bigcup_{i \isin \N} S_i$) ≤ $\displaystyle \sum_{i \isin \N}$φ($\displaystyle S_i$)成立   
>  
> 下面讨论 ∀ \' n ∈ $\displaystyle \N$ \'，有 \' ∃ C是可数集 且 C是$\displaystyle S_n$的覆盖 且 C ⊂ Y \' 的情形   
>   
> ∀"ε > 0","
>    
> ---             
>        
> ∀"n ∈ $\displaystyle \N$","    
> 将 正实数=$\displaystyle \frac{\varepsilon}{2^{1+n}}$ 应用到下确界的定理，有 ∃"M","M ∈ { $\displaystyle \sum_{A \isin C}$p(A) | C是可数集 且 C是$\displaystyle S_n$的覆盖 且 C ⊂ Y } 且 M < φ($\displaystyle S_n$) + $\displaystyle \frac{\varepsilon}{2^{n+1}}$"   
> 显然 /\* 涉及到选择公理 \*/，∃"$\displaystyle \text{C}_n$" /\* 记作$\displaystyle \text{C}_n$以强调与n的关联 \*/ ,"$\displaystyle \text{C}_n$是可数集 且 $\displaystyle \text{C}_n$是$\displaystyle\text{S}_n$的覆盖 且 $\displaystyle \text{C}_n$ ⊂ Y 且 $\displaystyle \sum_{\text{A} \isin \text{C}_n}$p(A) < φ($\displaystyle \text{S}_n$) + $\displaystyle \frac{\varepsilon}{2^{n+1}}$"           
> "   
>          
> 即 ∀"n ∈ $\displaystyle \N$","∃"$\displaystyle \text{C}_n$","$\displaystyle \text{C}_n$是可数集 且 $\displaystyle \text{C}_n$是$\displaystyle\text{S}_n$的覆盖 且 $\displaystyle \text{C}_n$ ⊂ Y 且 $\displaystyle \sum_{\text{A} \isin \text{C}_n}$p(A) < φ($\displaystyle \text{S}_n$) + $\displaystyle \frac{\varepsilon}{2^{n+1}}$""           
>    
> ---             
>       
> 从而，记K=$\displaystyle \bigcup_{n \isin \N} C_n$，有 K是可数集 且 K是$\displaystyle \bigcup_{n \isin \N} S_n$的覆盖 且 K ⊂ Y，从而 $\displaystyle \sum_{A \isin K}$p(A) ⊂ { $\displaystyle \sum_{A \isin C}$p(A) | C是可数集 且 C是$\displaystyle \bigcup_{n \isin \N} S_n$的覆盖 且 C ⊂ Y }   
> 根据φ的定义和下确界的定义，有 φ($\displaystyle \bigcup_{n \isin \N} S_n$) ≤ $\displaystyle \sum_{A \isin K}$p(A)    
> 由于 A∈K则一定有A∈某个$\displaystyle C_n$ 且 p非负，有$\displaystyle \sum_{A \isin K}$p(A) ≤ $\displaystyle \sum_{n \isin N} \sum_{A \isin C_n} \operatorname{p} (A)$   
> 又根据上文中已证明的结论，$\displaystyle \sum_{n \isin N} \sum_{A \isin C_n} \operatorname{p} (A)$ ≤ $\displaystyle \sum_{n \isin N} \displaystyle$ ( φ($\displaystyle S_n$) + $\displaystyle \frac{\varepsilon}{2^{n+1}}$ )，根据等比数列求和 $\displaystyle \sum_{n \isin N} \displaystyle$ ( φ($\displaystyle S_n$) + $\displaystyle \frac{\varepsilon}{2^{n+1}}$ ) ≤ $\displaystyle \sum_{n \isin N} \displaystyle$ φ($\displaystyle S_n$) + ε    
>"    
> 即 ∀ \' ε > 0 \'，有\' φ($\displaystyle \bigcup_{n \isin \N} S_n$) ≤ $\displaystyle \sum_{n \isin N} \displaystyle$ φ($\displaystyle S_n$) + ε \'，从而 φ($\displaystyle \bigcup_{n \isin \N} S_n$) ≤ $\displaystyle \sum_{n \isin N} \displaystyle$ φ($\displaystyle S_n$) \" //注： 根据\" ∀ \'ε > 0\'，有\'a ≤ b + ε\' \" 可以得出 \" a ≤ b \" //用反证法即可证明，假设 a > b，取 ε = $\displaystyle \frac{a-b}{2}$ > 0 即可得出矛盾    
>    
   
---   
卡拉西奥多里 //Caratheodory     

卡拉西奥多里准则(Caratheodory's Criterion) //可测性(Measurability)     
μ是X上的外测度 且 E ⊂ X ⇒ ( E是μ-可测的(μ-measurable) ⇔ ∀\"A ⊂ X\",有\"μ(A) = μ(A ∩ E) + μ(A ∩ $\displaystyle \complement_{X}$E)\" )      
\[陈天权 2009\] / 定义 9.4.1    

//一说\"μ(A) = μ(A ∩ E) + μ(A − E)\" //可以理解为用E将A“分割”开       

注：由于A = (A ∩ E) ∪ (A ∩ $\displaystyle \complement_{X}$E)，根据外侧度的定义(次可数可加性)，∀\"A ⊂ X\",有\"μ(A) ≤ μ(A ∩ E) + μ(A ∩ $\displaystyle \complement_{X}$E)\" 一定成立；因此，上述定义的等价形式为∀\"A ⊂ X\",有\"μ(A) ≥ μ(A ∩ E) + μ(A ∩ $\displaystyle \complement_{X}$E)\"   
  
注意，并集和差集并不能简单的理解成加法和减法    
B ∪ (A − B) = A ∪ B 而非 = A //可以直接从集合的定义证明，相等于证明 ∀\"a ∈ B ∪ (A − B)\"，有\"a ∈ A ∪ B\" 且 ∀\"a ∈ A ∪ B\"，有\"a ∈ B ∪ (A − B)\"       
~~//ProofWiki / Union with Superset is Superset~~     

可测集构成σ-代数 //Measurable Sets form Sigma-Algebra     
μ是X上的外测度 且 M = { E | E ⊂ X 且 E是μ-可测的 } ⇒ M是σ-代数    
\[Rudin 1976\] / 11.10 Theorem  
\[陈天权 2009\] / 定理 9.4.1       
\[Yeh 2014\] / Theorem 2.8    
      
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
> \= $\displaystyle \sum_{k=0}^{n}$(μ(A ∩ $\displaystyle \bigcup_{i = 0}^{k} E_i$) - μ(A ∩ $\displaystyle \bigcup_{i = 0}^{k-1} E_i$)) + μ(A - $\displaystyle \bigcup_{n \isin \N } E_n$) //裂项级数(Telescoping Series)       
> \= $\displaystyle \sum_{k=0}^{n}$(μ(A ∩ $\displaystyle \bigcup_{i = 0}^{k} E_i$) - μ(A ∩ $\displaystyle \bigcup_{i = 0}^{k} E_i$ ∩ $\displaystyle \bigcup_{i = 0}^{k-1} E_i$)) + μ(A - $\displaystyle \bigcup_{n \isin \N } E_n$) //因为$\displaystyle \bigcup_{i = 0}^{n-1} E_k$ ⊂ $\displaystyle \bigcup_{i = 0}^{n} E_k$               
> \= $\displaystyle \sum_{k=0}^{n}$μ((A ∩ $\displaystyle \bigcup_{i = 0}^{k} E_i$) − $\displaystyle \bigcup_{i = 0}^{k-1} E_i$) + μ(A - $\displaystyle \bigcup_{n \isin \N } E_n$) //将A = A ∩ $\displaystyle \bigcup_{i = 0}^{k} E_i$且E = $\displaystyle \bigcup_{i = 0}^{k-1} E_i$应用到定义"卡拉西奥多里准则，有μ((A ∩ $\displaystyle \bigcup_{i = 0}^{k} E_i$) = μ(A ∩ $\displaystyle \bigcup_{i = 0}^{k} E_i$ ∩ $\displaystyle \bigcup_{i = 0}^{k-1} E_i$)) + μ((A ∩ $\displaystyle \bigcup_{i = 0}^{k} E_i$) − $\displaystyle \bigcup_{i = 0}^{k-1} E_i$)      
> \= $\displaystyle \sum_{k=0}^{n}$μ(A ∩ ($\displaystyle \bigcup_{i = 0}^{k} E_i$ − $\displaystyle \bigcup_{i = 0}^{k-1} E_i$)) + μ(A - $\displaystyle \bigcup_{n \isin \N } E_n$)    
>      
> 由于对任意n ∈ $\displaystyle \N$成立，因此，在n趋向于$\displaystyle +\infty$时也成立，有 //\"n趋向于$\displaystyle +\infty$\"的这波操作在定义上可能缺乏严谨性，可能涉及到更高深的数学知识                   
> μ(A) ≥ $\displaystyle \sum_{k = 0 \land k \isin \N}^{+\infty}$μ(A ∩ ($\displaystyle \bigcup_{i = 0}^{k} E_i$ − $\displaystyle \bigcup_{i = 0}^{k-1} E_i$)) + μ(A - $\displaystyle \bigcup_{n \isin \N } E_n$)  
> ≥ μ(A ∩ (($\displaystyle \bigcup_{i = 0 \land i \isin \N}^{+\infty} E_i$ − $\displaystyle \bigcup_{i = 0 \land i \isin \N}^{+\infty-1} E_i$) ∪ ... ∪ ($\displaystyle \bigcup_{i = 0}^{0} E_i$ − ∅))) + μ(A - $\displaystyle \bigcup_{n \isin \N } E_n$)    
> \= μ(A ∩ $\displaystyle \bigcup_{n \isin \N} E_n$) + μ(A - $\displaystyle \bigcup_{n \isin \N } E_n$)     
> 从而 $\displaystyle \bigcup_{n \isin \N } E_n$ ∈ M //根据上文，由于≤一定成立，因此≥是=的充分必要条件(等价形式) //M对可数并集封闭       
>  

\[陈天权 2009\] / 定理 9.4.1       
\[Yeh 2014\] / Theorem 2.9  
μ是X上的外测度 且 M = { E | E ⊂ X 且 E是μ-可测的 } ⇒ u在M上可数可加    
//根据可数可加的定义，M是σ-代数是可数可加的前提   
    
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
