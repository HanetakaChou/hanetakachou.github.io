 关于如何进行证明：  
 
1\.全称量词的范围仅限于自然数集的命题，往往可以用数学归纳法（Induction）较便利地证明  

2\.形如“不存在..."的命题，往往可以用反证法（Contradiction）较便利地证明  

3\.其余情况，一般可以用演绎（Deductive）证明  
  
肯定前件 MP（Modus Ponens）  
  
hypothesis 假说/条件  
conclusion 结论  
statement 命题  
theorem 定理/真命题    
nontheorem 假命题    
negative 命题的否定 not(if p then q)  
inverse 否命题 if not p then not q  
converse 逆命题 if q then p 
contrapositive 逆否命题 if not q then not p  
counterexample 反例  
  
observation //也表示真命题(用于不含全称量词时)   

by symmetry //由于对称性 //同理可得  
  
A implies B //A能推出B    
whenever/if A holds, B follows/holds //当A成立时 B也成立      
A if and only if / iff  B //A当且仅当B  
A only if B //“仅当”（中文一般不用） //B是A的必要条件 即 A能推出B  
  
  
  
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
可以用归纳方式定义结构，比如自然数集就可以用归纳方式定义：  
Basis: 0是自然数  
Induction： 如果n是自然数，那么n+1也是自然数 //集合的集数/势 cardinality    

   

