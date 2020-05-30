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
   

柯西收敛准则（Cauchy's Convergence Test） 数列{xn}有极限的充分必要条件是：$\forall \, \epsilon > 0 , \, \exists \, N \isin \N^+ , \, \forall \, m > N , \, n > N , \, |x_m - x_n| < \epsilon$ //柯西极限存在准则/柯西审敛原理 //柯西完备性（Cauchy Completeness）    
      
    
### 极限（limit）    
  
去心领域 deleted neighborhood  

数列极限定义 //epsilon-delta definition  
if $\forall \, \epsilon > 0, \, \exists \, N \isin \N^+, \, \forall \, n > N, \, |x_n - a| < \epsilon$ then $\lim\limits_{x \rightarrow \infin}x_n = a$   

函数极限定义   
$\delta$    

证明极限  
对每个ϵ，求出相应的N //严格地来讲，只需证明N存在，并不需要给出N的具体值，但大多数情况下都能较便利地求出   
  
证明极限不存在  
给出反例ϵ 证明相应的N不存在（根据之前的总结，证明不存在往往可以用反证法） //严格地来讲，只需证明反例ϵ存在，并不需要给出ϵ的具体值，但大多数情况下都能较便利地求出  
  
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

有界性定理（Boundedness Theorem） //Robert Bartle, Donald Sherbert. "Introduction to Real Analysis, Fourth Edition" 2011 5.3.2 Boundedness Theorem  
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

极值定理（Extreme Value Theorem） //Robert Bartle, Donald Sherbert. "Introduction to Real Analysis, Fourth Edition" 2011 5.3.4 Maximum-Minimum Theorem  



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
   
  

