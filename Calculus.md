等价关系 等价类 商集 划分    

等价类要么相等要么不相交 //即不相等的等价类一定不相交   
证明： //参考： 定理3-10.1 定理3-10.2 离散数学 左孝凌  
反证法 //Proof by contradiction

假设 $a \isin [b]_\sim$ 、$a \isin [c]_\sim$ 且 $[b]_\sim \ne [c]_\sim$   
我们有 $a \sim b$ 、$a \sim c$ 由于$\sim$是等价关系 我们有$b \sim c$   

$\forall \, e \isin [b]_\sim$ 有$e \sim b$ 又因为$b \sim c$ 有$e \sim c$ 即$e \isin [c]_\sim$  
并且$\forall \, e \isin [c]_\sim$ 有$e \sim c$ 又因为$b \sim c$ 有$e \sim b$ 即$e \isin [b]_\sim$  
即$\forall \, e \, , \, e \isin [b]_\sim \Leftrightarrow e \isin [c]_\sim$ 即$[b]_\sim = [c]_\sim$ 但是，这与 $[b]_\sim \ne [c]_\sim$ 矛盾，命题得证 //事实上，可以证明：$b \sim c \Leftrightarrow [b]_\sim = [c]_\sim$    

最大数 max  
最小数 min    
有上界 （be） bounded above  
有下界 （be） bounded belowed    
上界 upper bound  
下界 lower bound  
上确界 supremum //最小上界 least upper bound       
下确界 infimum //最大下界 greatest lower bound    
  
Theroem 设M = supE，则 $\forall  \, \epsilon > 0, \, \exists \, x \isin E, \, x > M - \epsilon$    
Proof by Contradiction  
suppose $\exists \, x \isin E, \, x > M - \epsilon$ is not true  
then $\forall \, x \isin E, \, x <= M - \epsilon$, which implies $M - \epsilon$ is an upper bound of E  
since $\epsilon > 0$, $M - \epsilon$ is less than M, which contradicts the given statement "M is the least upper bound"  

Theroem 设M = supE，则 $\forall  \, \epsilon < 0, \, \exists \, x \isin E, \, x < M + \epsilon$  
证明从略   

实数完备性（Completeness of the real numbers） //实数系连续性  
  
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
又由于上界的定义 任意xn\<c 即xn-c\<0 由于ϵ>0 有xn-c<ϵ  
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
//\[同济大学数学系 2014\] / 第十二章 无穷级数 / 第三节 幂级数 / 二 幂级数及其收敛性 定理2    
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
  
指数函数定义： $\displaystyle \operatorname{exp}(x) = \sum_{n = 0}^{\infin} \frac{x^n}{n!}$  
//\[Rudin 1976\] / 8\.6 Theorem  
//\[陈天权 2009\] / 定义 3\.5\.2     

---  
  
$\displaystyle \operatorname{exp}(x) \cdot \operatorname{exp}(y) = \operatorname{exp}(x + y)$  
//\[Rudin 1976\] / 8\.6 Theorem   
//\[陈天权 2009\] / 定理 3\.5\.2       
   
证明：  
> $\displaystyle \operatorname{exp}(x) \cdot \operatorname{exp}(y)$    
= $\displaystyle \sum_{n=0}^\infin (\sum_{k=0}^n \frac{x^k \cdot y^{n-k}}{k! \cdot (n-k)!})$  
= $\displaystyle \sum_{n=0}^\infin (\frac{1}{n!} \sum_{k=0}^n \frac{n! \cdot x^k \cdot y^{n-k}}{k! \cdot (n-k)!})$  
= $\displaystyle \sum_{n=0}^\infin (\frac{1}{n!} \sum_{k=0}^n C_n^k \cdot x^k \cdot y^{n-k})$    
= $\displaystyle \sum_{n=0}^\infin \frac{ {(x + y)}^n }{n!}$ //逆用二项式定理      
= $\displaystyle \operatorname{exp}(x + y)$  
  
---  
   
根据 指数函数定义 $\displaystyle \operatorname{exp}(0) = 1$  
   
根据 欧拉数定义 $\displaystyle \operatorname{exp}(1) = \sum_{n=0}^\infin \frac{1}{n!} = e$  
   
可以证明 对任意实数x 有 $\displaystyle \operatorname{exp}(x) =  e^x$  //证明从略  

#### 三角函数（Trigonometric Functions）    
  
余弦定义：$\displaystyle \operatorname{cos}(x) = \frac{\operatorname{exp}(ix) + \operatorname{exp}(-ix)}{2}$  
  
正弦定义：$\displaystyle \operatorname{sin}(x) = \frac{\operatorname{exp}(ix) - \operatorname{exp}(-ix)}{2 i}$  

$\displaystyle \operatorname{exp}(ix) = 1 + ix - \frac{x^2}{2!} - \frac{ix^3}{3!} + \frac{x^4}{4!} + ...$  //i -1 -i 1  

$\displaystyle \operatorname{exp}(-ix) = 1 -ix - \frac{x^2}{2!} + \frac{ix^3}{3!} + \frac{x^4}{4!} + ...$  //-i -1 i 1  

$\displaystyle \operatorname{cos}(x) = 1 - \frac{x^2}{2!} + \frac{x^4}{4!} + ...$  

$\displaystyle \operatorname{sin}(x) = x - \frac{x^3}{3!} + \frac{x^5}{5!} + ...$  
  
$\displaystyle \operatorname{exp}(ix) = \operatorname{cos}(x) + i\operatorname{sin}(x)$  
  
  
### 极限（limit）    

虽然 数列可以认为是一种特殊的函数  
但是 数列极限却不可以认为是一种特殊的函数极限 //在函数极限的定义中 要求函数在去心领域上有定义 而去心领域包含一段连续的实数 这是数列所不具备的   

去心领域 deleted neighborhood    
领域 neighborhood  
  
函数极限定义 //epsilon-delta definition   
$\delta$    
  
Sequential Criterion for Limits //函数极限与数列极限的关系 //Robert Bartle, Donald Sherbert. "Introduction to Real Analysis, Fourth Edition" 4.1.8 Theorem  
函数f(x)在x0处的极限为A 数列{xn}的极限为x0 且 存在N，当n>N时，有xn≠x0 -> 数列{f(xn)}的极限为A  

函数极限的局部有界性 //Robert Bartle, Donald Sherbert. "Introduction to Real Analysis, Fourth Edition" 4.1.8 Theorem  

极限运算法则  
根据定义求极限的效率太低，因此引入了极限运算法则，但是这也是出错的开始  

商法则  //分母不能为0   
复合函数  //存在去心邻域 满足g(x)不等于极限  

有理整函数（polynomial function） 或 (代入后分母不等于零的)有理分式函数（rational function） 直接代入即极限 //为提供证明 后文会扩充到初等函数     
  
根据定义易知 对函数进行的恒等变形（比如“约分”等） 只要 存在某个去心邻域 能使相应的恒等变形成立 即可  

~~单调收敛原理/单调收敛定理（Monotone Convergence Theorem） 单调有界数列必有极限 //仅适用于数列 且不能求出极限的具体值~~    
  
夹逼准则（Squeeze Theorem） //由于效率较低，在求函数极限时，一般借助于初等函数的连续性，并不常用 //但求数列极限的方法较少，可能会用到夹逼准则  

~~柯西收敛准则 Cauchy's convergence test //柯西极限存在准则/柯西审敛原理~~  

$\lim\limits_{x \rightarrow  0}\frac{\sin ( x ) }{x} = 1$   

$\lim\limits_{x \rightarrow \infin} {( 1 + \frac{1}{x} )}^x = e$  
$=\lim\limits_{x \rightarrow \infin} e^{ ( \ln ( { ( 1 + \frac{1}{x} ) } ^ x ) ) }$  
$=\lim\limits_{x \rightarrow \infin} e^{ ( x \ln ( 1 + \frac{1}{x} ) ) }$  
$=\lim\limits_{x \rightarrow \infin} e^{ \frac{\ln ( 1 + \frac{1}{x} )}{\frac{1}{x}} }$  
$=\lim\limits_{x \rightarrow 0} e^{ \frac{\ln ( 1 + x )}{x} }$  

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
if $\lim\limits_{x \rightarrow x_0} \operatorname{f}(x) = \operatorname{f}(x_0)$ then f(x)在$x_0$处连续     

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
//参考 陈天权 "数学分析讲义" 第一册 定理4.2.2  
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


### 测度（Measure）  


### 积分（Integral）    

定积分/黎曼积分 Riemann Integral  
反常积分/广义积分  Henstock–Kurzweil Integral/Generalized Riemann Integral  

换元积分法 Integration by Substitution  
分部积分法 Integration by Parts  

第一类换元法  
如果g(x)可以写成g(x)=f\[φ(x)\]φ'(x)的形式  
那么$\int_a^b g(x) \, dx = \int_{\phi(a)}^{\phi(b)} f(u) \, du$  

证明  
设F(u)是f(u)的原函数  
$\int_{\phi(a)}^{\phi(b)} f(u) \, du$ = F\[φ(b)\]  - F\[φ(a)\] （等式1）  

设G(x)=F\[φ(x)\]  
**有G'(x)=F'\[φ(x)\]φ'(x)=f\[φ(x)\]φ'(x) => 因此G(x)是g(x)的原函数** //证明的关键     
$\int_a^b g(x) \, dx$ = G(b) - G(a) = F\[φ(b)\]  - F\[φ(a)\] （等式2）

结合（等式1）（等式2），我们有$\int_a^b g(x) \, dx = \int_{\phi(a)}^{\phi(b)} f(u) \, du$，命题得证  
   
第二类换元法  
   
  
### 参考文献  
\[Bartle 2011\] Robert Bartle, Donald Sherbert. "Introduction to Real Analysis, Fourth Edition." Wiley 2011.   
\[Rudin 1976\] Walter Rudin. "Principles of Mathematical Analysis, Third Edition." McGraw-Hill 1976.   
\[陈天权 2009\] 陈天权. "数学分析讲义." 北京大学出版社 2009.  
