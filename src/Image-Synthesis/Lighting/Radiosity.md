# Radiosity  

## Radiant Existance  
The term **radiosity B** is a deprecated term which was popular in the last century, and currently should be called **radiant exitance M** instead which denotes the **outgoing** **irradiance E**.  

The terms **irradiance E** and **form factor F** may be used interchangeably, but technically **irradiance E** should NOT be divided by $\displaystyle \pi$. This means that $\displaystyle \operatorname{E} = \pi \operatorname{F}$.

However, to be consistent with the most literature on the [Radiosity](https://en.wikipedia.org/wiki/Radiosity_(computer_graphics)) global illumination algorithm, the term **radiosity B** rather than **radiant exitance M** is used here.  

## FEM (Finite Element Method)  

$\frac{B{\lparen x \rparen}}{\pi} = \frac{E{\lparen x \rparen}}{\pi} + \int_{All\,x'} \frac{\rho{\lparen x\rparen}}{\pi} \frac{B{\lparen x'\rparen}}{\pi} \frac{\cos\theta_i\cos\theta_o}{{\vert x'-x\vert}^2} V{\lparen x'\rarr x \rparen} \, dA'$  

$B{\lparen x \rparen} = E{\lparen x \rparen} + \rho{\lparen x\rparen}\, \int_{All\,x'} \frac{1}{\pi} B{\lparen x'\rparen} \frac{\cos\theta_i\cos\theta_o}{{\vert x'-x\vert}^2} V{\lparen x'\rarr x \rparen} \, dA'$  //no longer directional   

By "2.8 Method of Weighted Residuals" and "2.9 Introduction to Finite Elements" of [16.90 Computational Methods in Aerospace Engineering](https://mitocw.ups.edu.ec/courses/aeronautics-and-astronautics/16-90-computational-methods-in-aerospace-engineering-spring-2014/#), 


$\hat{B}{\lparen x \rparen} = \sum_{i=1}^n {B_i N_i{\lparen x \rparen}}$  

Residual  
$r{\lparen x \rparen} = \hat{B}{\lparen x \rparen} - E{\lparen x \rparen} - \rho{\lparen x\rparen}\, \int_{All\,x'} \frac{1}{\pi} \hat{B}{\lparen x'\rparen} \frac{\cos\theta_i\cos\theta_o}{{\vert x'-x\vert}^2} V{\lparen x'\rarr x \rparen} \, dA'$  
  
Weighted Residual  

Let $W_i{\lparen x \rparen} = N_i{\lparen x \rparen}$  
$\int_{All\,x}{r{\lparen x \rparen} W_i{\lparen x \rparen}}\, dA$ //project to  $W_i{\lparen x \rparen}$  
$= \int_{All\,x}{ {\lbrack \hat{B}{\lparen x \rparen} - E{\lparen x \rparen} - \rho{\lparen x\rparen}\, \int_{All\,x'} \frac{1}{\pi} \hat{B}{\lparen x'\rparen} \frac{\cos\theta_i\cos\theta_o}{{\vert x'-x\vert}^2} V{\lparen x'\rarr x \rparen} \, dA' \rbrack} N_i{\lparen x \rparen}  }\, dA$  
$= \int_{All\,x}{\hat{B}{\lparen x \rparen} N_i{\lparen x \rparen}}\, dA - \int_{All\,x}{E{\lparen x \rparen} N_i{\lparen x \rparen}}\, dA - \int_{All\,x}{ {\lbrack \rho{\lparen x\rparen}\, \int_{All\,x'} \frac{1}{\pi} \hat{B}{\lparen x'\rparen} \frac{\cos\theta_i\cos\theta_o}{{\vert x'-x\vert}^2} V{\lparen x'\rarr x \rparen} \, dA' \rbrack} N_i{\lparen x \rparen}  }\, dA$  
$= \int_{All\,x}{ {\lbrack \sum_{j=1}^n {B_j N_j{\lparen x \rparen}} \rbrack} N_i{\lparen x \rparen}}\, dA - \int_{All\,x}{E{\lparen x \rparen} N_i{\lparen x \rparen}}\, dA - \int_{All\,x}{ {\lbrace \rho{\lparen x\rparen}\, \int_{All\,x'} \frac{1}{\pi} {\lbrack \sum_{j=1}^n {B_j N_j{\lparen x \rparen}} \rbrack} \frac{\cos\theta_i\cos\theta_o}{{\vert x'-x\vert}^2} V{\lparen x'\rarr x \rparen} \, dA' \rbrace} N_i{\lparen x \rparen}  }\, dA$   
$= \sum_{j=1}^n {\lbrack \int_{All\,x}{ B_j N_j{\lparen x \rparen} N_i{\lparen x \rparen}}\, dA \rbrack} - \int_{All\,x}{E{\lparen x \rparen} N_i{\lparen x \rparen}}\, dA - \int_{All\,x}{ {\lbrace \rho{\lparen x\rparen} \sum_{j=1}^n {\lbrack \int_{All\,x'} \frac{1}{\pi} B_j N_j{\lparen x \rparen} \frac{\cos\theta_i\cos\theta_o}{{\vert x'-x\vert}^2} V{\lparen x'\rarr x \rparen} \, dA' \rbrack} \rbrace} N_i{\lparen x \rparen}  }\, dA$ //linear  
$= \sum_{j=1}^n B_j {\lbrack \int_{All\,x}{ N_j{\lparen x \rparen} N_i{\lparen x \rparen}}\, dA \rbrack} - \int_{All\,x}{E{\lparen x \rparen} N_i{\lparen x \rparen}}\, dA - \int_{All\,x}{ {\lbrace \rho{\lparen x\rparen} \sum_{j=1}^n B_j {\lbrack \int_{All\,x'} \frac{1}{\pi} N_j{\lparen x \rparen} \frac{\cos\theta_i\cos\theta_o}{{\vert x'-x\vert}^2} V{\lparen x'\rarr x \rparen} \, dA' \rbrack} \rbrace} N_i{\lparen x \rparen}  }\, dA$ //$B_j$ is constant  
$= \sum_{j=1}^n B_j {\lbrack \int_{All\,x}{ N_j{\lparen x \rparen} N_i{\lparen x \rparen}}\, dA \rbrack} - \int_{All\,x}{E{\lparen x \rparen} N_i{\lparen x \rparen}}\, dA - \sum_{j=1}^n {\lbrace \int_{All\,x}{ {\lbrack \rho{\lparen x\rparen} B_j \int_{All\,x'} \frac{1}{\pi} N_j{\lparen x \rparen} \frac{\cos\theta_i\cos\theta_o}{{\vert x'-x\vert}^2} V{\lparen x'\rarr x \rparen} \, dA' \rbrack} N_i{\lparen x \rparen}  }\, dA \rbrace}$ //linear  
$= \sum_{j=1}^n B_j {\lbrack \int_{All\,x}{ N_j{\lparen x \rparen} N_i{\lparen x \rparen}}\, dA \rbrack} - \int_{All\,x}{E{\lparen x \rparen} N_i{\lparen x \rparen}}\, dA - \sum_{j=1}^n B_j {\lbrace \int_{All\,x}{ {\lbrack \rho{\lparen x\rparen} \int_{All\,x'} \frac{1}{\pi} N_j{\lparen x \rparen} \frac{\cos\theta_i\cos\theta_o}{{\vert x'-x\vert}^2} V{\lparen x'\rarr x \rparen} \, dA' \rbrack} N_i{\lparen x \rparen}  }\, dA \rbrace}$ //$B_j$ is constant  
$= B_i A_i - \int_{A_i}{E{\lparen x \rparen}}\, dA - \sum_{j=1}^n B_j {\lbrace \int_{A_i}{ {\lbrack \rho{\lparen x\rparen} \int_{A_j} \frac{1}{\pi} \frac{\cos\theta_i\cos\theta_o}{{\vert x'-x\vert}^2} V{\lparen x'\rarr x \rparen} \, dA' \rbrack} }\, dA \rbrace}$ //Additive Interval Property //By FEM, other intervals should be 0    
$= B_i A_i - E_i A_i - \sum_{j=1}^n B_j \rho_i {\lbrace \int_{A_i}{ {\lbrack \int_{A_j} \frac{1}{\pi} \frac{\cos\theta_i\cos\theta_o}{{\vert x'-x\vert}^2} V{\lparen x'\rarr x \rparen} \, dA' \rbrack} }\, dA \rbrace}$ //$E_i$ is the average value on $A_i$ //assume $\rho{\lparen x\rparen}$ is the same on $A_i$, namely, is constant
