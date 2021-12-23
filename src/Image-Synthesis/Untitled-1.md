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
> 结合（等式1）（等式2），我们有$\displays