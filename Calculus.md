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
  
LUB公理 //直接看作公理   

戴德金性质（Dedekind Property） R的划分A|B 满足A中的数都小于B， 一定有 A有最大数 或 B有最小数 //戴德金定理  
>证明：  
>任取B中的某个实数，即为A的上界 即A的上界存在 根据LUB公理，A的上确界存在，不妨设w=supA  
由于A|B是R的划分，必有w属于A或w属于B  
根据w属于A和w属于B分类讨论  
w属于A  
即A中有最大数w，命题成立  
w属于B  
显然，对于任意y属于B，有y是A的上界 
由于w是A的最小上界 w是B的最小数    

最大下界原理 有下界的非空实数集一定有下确界  
>证明：  
>H = { y属于R : y是S的下界 }  
K = { y属于R : y不是S的下界 }  
由于下界存在 H非空 (H|K)是R的划分   
显然 H中的数都小于K   
根据 戴德金性质 H有最大数 或 K有最小数   
用反证法证明 K没有最小数  
不妨设K有最小数b 由于b不是S的下界 存在某个小于b且属于S的实数，不妨设为a  
显然(a+b)/2 > a 即(a+b)/2不是S的下界 即(a+b)/2属于K 但是(a+b)/2 < b，这与b是K的最小数矛盾  

单调收敛定理（Monotone Convergence Theorem） 单调有界数列必有极限 //单调收敛原理    
>  
>单调递增 monotonically increasing  
>单调递减 monotonically decreasing  
>   
>证明 单调递增情形  
由于{xn}有界 根据LUB公理 {xn}有上确界，不妨设c=sup{xn}  
根据上确界性质 对任意ϵ>0 存在a属于{xn} 满足a>c-ϵ 不妨设a的下标为A 即a=xA   
由于{xn}单调递增 取N=A 对任意n>N 满足xn>xN=xA>c-ϵ 即xn-c>-ϵ  
又由于上界的定义 任意xn\<c 即xn-c\<0 由于ϵ>0 有xn-c<ϵ  
综上|xn-c|<ϵ 命题得证   
   
区间套原理（Nested Intervals Theorem）  
闭区间序列$\{[a_n, b_n]\}$满足$\forall n \isin \N^+ , \,  [a_n, b_n] \supe [a_{n+1},b_{n+1}]$，一定有 $\exists \, \zeta, \eta \isin \R , \, \cap_{n=1}^\infin [a_n, b_n] = \{ x : \zeta \le x \le \eta \}$  
//注：所有闭区间的交集$\cap_{n=1}^\infin [a_n, b_n]$可以严谨地表示为$\{ x : \forall n \isin \N^+ , \,  x \isin [a_n, b_n] \}$    
//当$\zeta \ne \eta$时，$\{ x : \zeta \le x \le \eta \}$为闭区间$[\zeta, \eta]$；当$\zeta = \eta$时，$\{ x : \zeta \le x \le \eta \}$退化为某一实数  
>证明：  
>  
>根据题意，我们有 a1<=a2<=......<=an<=......<=bn<=......<=b2<=b1  
显然 数列{an}单调递增且有界（比如：b1是{an}的一个上界） 数列{bn}单调递减且有界（比如：a1是{bn}的一个下界）      
根据 单调收敛定理 不妨设ζ=sup{an} η=inf{bn} 我们有 {an}收敛于ζ {bn}收敛于η  
>
>接下来用反证法证明ζ<=η  
假设ζ>η  
由于ζ是{an}的上确界 不妨取ϵ=(ζ-η)/2 根据上确界性质 存在aA属于{an} 满足aA > ζ-ϵ = (ζ+η)/2  
由于η是{bn}的下确界 不妨取ϵ=(ζ-η)/2 根据下确界性质 存在bB属于{bn} 满足bB < η+ϵ = (ζ+η)/2  
综上，即 存在 aA属于{an} bB属于{bn} 满足 aA > bB //显然，这与题意矛盾  
>
>由于 对任意n 都有an<=ζ<=η<=bn成立 我们有$\{ x : \zeta \le x \le \eta \} \sube \cap_{n=1}^\infin [a_n, b_n]$成立  
接下来 只要证明$\cap_{n=1}^\infin [a_n, b_n] \sube \{ x : \zeta \le x \le \eta \}$ 命题即得证  
我们用反证法证明  
假设x属于$\cap_{n=1}^\infin [a_n, b_n]$且x不属于$\{ x : \zeta \le x \le \eta \}$  
对x<ζ和x>η两种情形分类讨论  
当x<ζ时  
不妨取ϵ=(ζ-x) 根据上确界性质 存在aK属于{an} 满足aK > ζ-ϵ = x 即x不属于\[ak,bK\] 但是，这与x属于$\cap_{n=1}^\infin [a_n, b_n]$矛盾  
当x>η时
证明从略  



柯西收敛准则（Cauchy's Convergence Test） 数列{xn}有极限的充分必要条件是：$\forall \, \epsilon > 0 , \, \exists \, N \isin \N^+ , \, \forall \, m > N , \, n > N , \, |x_m - x_n| < \epsilon$ //柯西极限存在准则/柯西审敛原理 //柯西完备性（Cauchy Completeness）    
      
    
### 极限（limit）    
  
极限定义 //epsilon-delta definition  
if $\forall \, \epsilon > 0, \, \exists \, N \isin \N^+, \, \forall \, n > N, \, |x_n - a| < \epsilon$ then $\lim\limits_{x \rightarrow \infin}x_n = a$   
  
证明极限  
对每个ϵ，求出相应的N //严格地来讲，只需证明N存在，并不需要给出N的具体值，但大多数情况下都能较便利地求出   
  
证明极限不存在  
给出反例ϵ 证明相应的N不存在（根据之前的总结，证明不存在往往可以用反证法） //严格地来讲，只需证明反例ϵ存在，并不需要给出ϵ的具体值，但大多数情况下都能较便利地求出  
  
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

连续函数的性质

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

区间 interval  
开区间 open interval  
闭区间 closed interval  
半开区间 half-open interval  

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
   
  

