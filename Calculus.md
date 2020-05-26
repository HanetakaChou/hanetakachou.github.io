等价关系 等价类 商集 划分    

等价类要么相等要么不相交 //即不相等的等价类一定不相交   
证明： //参考： 定理3-10.1 定理3-10.2 离散数学 左孝凌  
反证法 //Proof by contradiction

假设 $a \isin [b]_\sim$ 、$a \isin [c]_\sim$ 且 $[b]_\sim \ne [c]_\sim$  
我们有 $a \sim b$ 、$a \sim c$ 由于$\sim$是等价关系 我们有$b \sim c$   

$\forall \, e \isin [b]_\sim$ 有$e \sim b$ 又因为$b \sim c$ 有$e \sim c$ 即$e \isin [c]_\sim$  
并且$\forall \, e \isin [c]_\sim$ 有$e \sim c$ 又因为$b \sim c$ 有$e \sim b$ 即$e \isin [b]_\sim$  
即$\forall \, e \, , \, e \isin [b]_\sim \Leftrightarrow e \isin [c]_\sim$ 即$[b]_\sim = [c]_\sim$ 但是，这与 $[b]_\sim \ne [c]_\sim$ 矛盾，命题得证 //事实上$b \sim c \Leftrightarrow [b]_\sim = [c]_\sim$    


戴德金分割（Dedekind cut）  
  
实数完备性（Completeness of the real numbers） //实数系连续性  

戴德金完备性（Dedekind completeness）  
最小上界性（Least Upper Bound Property） //LUB公理  
  
柯西完备性（Cauchy completeness）
柯西收敛准则（Cauchy's convergence test） //柯西极限存在准则/柯西审敛原理  
  
区间套原理（Nested intervals theorem）  
  
单调收敛定理（Monotone Convergence Theorem） //单调收敛原理    
  
单调递增 monotonically increasing  
单调递减 monotonically decreasing  
   
### 极限（limit）    
  
极限定义 //epsilon-delta definition  
if $\forall \, \epsilon > 0, \, \exists \, N \isin \natnums^+, \, \forall \, n > N, \, |x - a| < \epsilon$ then $\lim\limits_{x \rightarrow \infin}x_n = a$   
  
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
   
  

