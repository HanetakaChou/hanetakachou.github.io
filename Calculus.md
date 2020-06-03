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
上界 upper bound
上确界 supremum //最小上界 least upper bound       
下确界 infimum //最大下界   
  
Theroem 设M = supE，则 $\forall  \, \epsilon > 0, \, \exists \, x \isin E, \, x > M - \epsilon$    
Proof by Contradiction  
suppose $\exists \, x \isin E, \, x > M - \epsilon$ is not true  
then $\forall \, x \isin E, \, x <= M - \epsilon$, which implies $M - \epsilon$ is an upper bound of E  
since $\epsilon > 0$, $M - \epsilon$ is less than M, which contradicts the given statement "M is the least upper bound"  

Theroem 设M = supE，则 $\forall  \, \epsilon < 0, \, \exists \, x \isin E, \, x < M + \epsilon$  
证明从略   

实数完备性（Completeness of the real numbers） //实数系连续性  
  
最小上界性（Least Upper Bound Property）有上界的非空实数集一定有上确界 //戴德金完备性（Dedekind Completeness）     
LUB公理（LUB Axiom) //直接看作公理   
  
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
数列{xn}有极限的充分必要条件是：$\exists \ \Leftrightarrow \forall \, \epsilon > 0 , \, \exists \, N \isin \N^+ , \, \forall \, m > N , \, n > N , \, |x_m - x_n| < \epsilon$   
//Robert Bartle, Donald Sherbert. "Introduction to Real Analysis, Fourth Edition" 2011 / 3.5.5 Cauchy Convergence Criterion  
>证明  
>  
> 必要性 //Necessary    
let lim Xn = a  
for all given ϵ > 0  
by the definition of the limit of a sequence, there exists a K(ϵ/2) ∈ N such that for all n > K(ϵ/2) ∈ N, we have |xn - a| < ϵ/2    
let H(ϵ) = K(ϵ/2)   
for all n,m > H(ϵ),  we have |xn - xm| = |(xm - a) - (xn -a)| =


充分性 //Sufficiency  
    
### e（Euler's number）   
$e = \lim\limits_{n \rightarrow \infin} (1+\frac{1}{n})^n$  
$e = \displaystyle{\sum_{n=0}^\infin} \frac{1}{n!} = 1 + 1 + \frac{1}{1 \cdot 2} +  \frac{1}{1 \cdot 2 \cdot 3} + ...$  


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
数列{sn}的极限称为级数的和（sum）或值（value） //通常记作$\displaystyle{\sum_{n=1}^\infin} x_n$   

调和级数（Harmonic Series）  
$\displaystyle{\sum_{n=1}^\infin} \frac{1}{n} = 1 + \frac{1}{2} + \frac{1}{3} + ... + \frac{1}{n} + ...$   

几何级数（Geometric Series） //等比数列部分和  
$\displaystyle{\sum_{n=0}^\infin} r^n = 1 + r + r^2 + ... + r^n + ...$   

##### 级数收敛的必要条件  
The nth Term Test //\[Bartle 2011\] \\ 3\.7\.3 The nth Term Test  
级数收敛的必要条件 //\[同济大学数学系 2014\] 第十二章 无穷级数 / 第一节 常数项级数的概念和性质 / 二 收敛级数的基本性质 性质5  

级数 $\displaystyle{\sum_{n = 1}^\infin} x_n$ 收敛 $\Rightarrow \lim\limits_{n \rightarrow \infin}x_n = 0$  
>Proof //证明  
let $\displaystyle{\sum_{n = 1}^\infin} x_n = a$ and $s_n = \displaystyle{\sum_{k = 1}^n} x_k$   
then $\lim\limits_{n \rightarrow \infin} x_n = \lim\limits_{n \rightarrow \infin} (s_n - s_{n-1}) = \lim\limits_{n \rightarrow \infin} s_n - \lim\limits_{n \rightarrow \infin} s_{n-1} = a - a = 0$ //数列极限的运算法则  

##### 柯西审敛原理  
Cauchy's convergence test //Wikipedia  
Cauchy Criterion for Series //\[Bartle 2011\] \\ 3\.7\.4 Cauchy Criterion for Series  
柯西审敛原理 //\[同济大学数学系 2014\] 第十二章 无穷级数 / 第一节 常数项级数的概念和性质 / 三 柯西审敛原理  
级数 $\displaystyle{\sum_{n = 1}^\infin} x_n$ 收敛 $\Leftrightarrow \forall \, \epsilon > 0, \, \exists \, H(\epsilon) \isin \N, \, \forall \, m > n \ge H(\epsilon), \, |\displaystyle{\sum_{k = n}^m} x_n| < \epsilon$    
//由于级数本身也是一种数列 将 对数列的柯西审敛原理 应用至此即可   

##### 正项级数及其审敛法 //非负项级数    
正项级数 //let xn be a sequence of nonnegative real numbers //零或正数  

正项级数收敛 ⇔ 部分和数列有界 //\[Bartle 2011\] \\ 3\.7\.5 Theorem  
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

##### 交错级数及其审敛法  

交错调和级数 （Alternating Harmonic Series） $\displaystyle{\sum_{n = 1}^\infin} \frac{{(-1)}^{n+1}}{n}$ 收敛  
> 证明  
> 
>      

##### 绝对收敛与条件收敛

### 函数项级数（Series of Functions）  

##### 函数项数列（Sequences of Functions）  
//函数项数列fn(x)在A上逐点（Pointwise）收敛 //$\operatorname{f_n}(x) \rightarrow \operatorname{f}(x)$ on A   
$\forall \, x \isin A , \, \lim\limits_{n \rightarrow \infin} \operatorname{f_n}(x) = \operatorname{f}(x)$ //对给定x，fn(x)即常数项数列   
$\forall \, \epsilon > 0 , \, x \isin A , \, \exists \, K(\epsilon , \, x) \isin \N , \, \forall \, n > K(\epsilon , \, x) , \, |\operatorname{f_n}(x) - \operatorname{f}(x)| < \epsilon$ ⇔ $\operatorname{f_n}(x) \rightarrow \operatorname{f}(x)$ on A  
  
//函数项数列fn(x)在A上一致（Uniform）收敛 //$\operatorname{f_n}(x) \rightrightarrows \operatorname{f}(x)$ on A    
$\forall \, \epsilon > 0 , \, \exists \, K(\epsilon) \isin \N , \, \forall \, n > K(\epsilon)  , \, x \isin A , \, |\operatorname{f_n}(x) - \operatorname{f}(x)| < \epsilon$ ⇔ $\operatorname{f_n}(x) \rightrightarrows \operatorname{f}(x)$ on A  

##### 函数项级数（Series of Functions）  
\[Bartle 2011\] 基于 函数项数列的逐点收敛 定义 函数项级数  


##### 幂级数（Power Series）  
$\displaystyle{\sum_{n = 0}^{\infin}} a_nx^n$ = $a_0 + a_1x + ... + + a_nx^n + ...$        

收敛半径 radius of convergence  
Cauchy-Hadamard Theorem  

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


### 导数（Derivative）

洛必达法则（L'Hôpital's rule）  


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
\[Bartle 2011\] Robert Bartle, Donald Sherbert. "Introduction to Real Analysis, Fourth Edition" 2011.   
\[陈天权 2009\] 陈天权. "数学分析讲义 第一册" 2009.  
\[Rudin 1964\] Walter Rudin. "Principles of Mathematical Analysis, Third Edition." McGraw-Hill 1964.  
  