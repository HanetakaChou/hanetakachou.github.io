 关于如何进行证明：  
 
1\.全称量词的范围仅限于自然数集的命题，往往可以用数学归纳法（Induction）较便利地证明  

2\.形如“不存在..."的命题，往往可以用反证法（Contradiction）较便利地证明  

3\.其余情况，一般可以用演绎（Deductive）证明  

hypothesis 假说/条件  
conclusion 结论  
statement 命题  
theorem 定理/真命题    
nontheorem 假命题    
negative 否命题  
converse 逆命题  
inverse //中文不存在  
contrapositive 逆否命题  
counterexample 反例  

A implies B //A能推出B  


**数学归纳法（proof by induction）**

**Integer Induction - 一般形式**

to prove $\forall \, n \isin \natnums^+, \, S(n)$  

just to prove:  
1\.basis: 证明S(0)成立  
2\.inductive step: 当S(n)成立时，证明S(n+1)也成立 

**Interger Induction - More General Forms（广义形式）**  
1\.basis //可以有多个basis case    
2\.inductive step  //在证明S(n+1)为真时 不仅是S(n),还有S(n-1)...S(0)都可以用于推导  

**Structural Induction（结构归纳法）**  
实际上不仅是自然数集，只要是递归定义的概念 都可以用数学归纳法证明    
集合的集数/势 cardinality    

   

