### 极限  
  
极限定义  
if $\forall \, \epsilon > 0, \, \exists \, N \isin \natnums^+, \, \forall \, n > N, \, |x - a| < \epsilon$ then $\lim\limits_{x \rightarrow \infin}x_n = a$   

证明极限  
对每个ϵ，求出相应的N //严格地来讲，只需证明N存在，并不需要给出N的具体值，但大多数情况下都能较便利地求出   

证明极限不存在  
给出反例ϵ 证明相应的N不存在（根据之前的总结，证明不存在往往可以用反证法） //严格地来讲，只需证明反例ϵ存在，并不需要给出ϵ的具体值，但大多数情况下都能较便利地求出  

极限运算法则  
根据定义求极限的效率太低，因此引入了极限运算法则，但是这也是出错的开始  

商法则  //分母不能为0   
复合函数  //存在去心邻域 满足g(x)不等于极限  

有理整函数 或 (代入后分母不等于零的)有理分式函数 直接代入即极限 //未提供证明 却一直再用   

根据定义易知 对函数进行的恒等变形（比如“约分”等） 只要 存在某个去心邻域 能使相应的恒等变形成立 即可  

夹逼准则（Squeeze Theorem） //效率较低 //实际中不常用 //思路上一般是借助有理整函数 

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


无穷小 Infinitesimal  

等价无穷小代替 提升效率  

sinx ~ x  
1 - cosx ~ 1/2 x^2
~ 1/n


等价无穷小具有传递性 //等价类  
