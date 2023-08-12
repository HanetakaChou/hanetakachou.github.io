# Radiosity

## FEM (Finite Element Method)  

Let $\displaystyle \operatorname{f}(x)$ be the solution of a **differential equation** which can be written as $\displaystyle \operatorname{f}(x) = P(x)$.  

The main idea of **FEM(Finite Element Method)** is to convert the **infinite** problem of solving a **differential equation** to the **finite** problem of solving a **system of equations**.  

We try to approximate $\displaystyle \operatorname{f}(x)$ with the **basis functions** $\displaystyle \sum_{k=1}^n f_k \operatorname{v_k}(x)$.  
The idea of the basis functions in **FEM** is similar to **SH (Spherical Harmonics)** or **Fourier**. But the basis functions in **FEM** are NOT forced to be **orthonormal**.  
Actually, the aim of the **FEM** is usually to discretize the domain of $\displaystyle \operatorname{f}(x)$, and the basis functions in FEM is much simpler than in **SH** or **Fourier**. For example, when the domain of $\displaystyle \operatorname{f}(x)$ is [0, 1], let $\displaystyle \operatorname{v_1}(x) = {\begin{cases} 1 &{x \isin [0, \frac{1}{2}]} \\0 &{x \isin [\frac{1}{2}, 1]} \end{cases}}$ and $\displaystyle \operatorname{v_2}(x) = {\begin{cases} 0 &{x \isin [0, \frac{1}{2}]} \\1 &{x \isin [\frac{1}{2}, 1]} \end{cases}}$, evidently $\displaystyle \operatorname{v_1}(x)$ and $\displaystyle \operatorname{v_2}(x)$ are **orthogonal**.  

Let $\displaystyle \operatorname{r}(x) = \sum_{k=1}^n f_k \operatorname{v_k}(x) - \operatorname{f}(x) = \sum_{k=1}^n f_k \operatorname{v_k}(x) - P(x)$ be the **residual**.  
The projection of the **residual** on each basis function should be zero. This means that $\displaystyle \int \operatorname{r}(x) \operatorname{v_k}(x) = 0 \, (k = 1 \ldots n)$ (of which the $\displaystyle \operatorname{R}(x) = \operatorname{r}(x) \operatorname{v_k}(x)$ is also called the **weighted residual**). And we have the **system of equations** about the coefficients $\displaystyle f_k$.  
