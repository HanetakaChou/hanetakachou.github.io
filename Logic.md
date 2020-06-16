 关于如何进行证明：  
 
1\.全称量词的范围仅限于自然数集的命题，往往可以用数学归纳法（Induction）较便利地证明  

2\.形如“不存在..."的命题，往往可以用反证法（Proof by Contradiction）较便利地证明  

3\.其余情况，一般可以用演绎（Deductive）证明  
  
肯定前件 MP（Modus Ponens）  

axiom 公理  
  
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

necessity 必要性  
sufficiency 充分性  
  
observation //也表示真命题(用于不含全称量词时)   

by symmetry //由于对称性 //同理可得  
  
since //由于 //因为    
by //根据（...定理)    

evident //显然   

it follows that //因此 //所以   

and / but //且   

we have shown that //我们已经证明 //我们得到  

in other words //即  
this means that //这意味着/即

let //不妨设  
call it a //将它称作a  


we have (that) //我们有  
it holds that //...成立  
  
A implies B //A能推出B    
whenever/if A holds, B follows/holds //当A成立时 B也成立      
A if and only if / iff  B //A当且仅当B  
A only if B //“仅当”（中文一般不用） //B是A的必要条件 即 A能推出B  
  
**数学归纳法（proof by induction）**  
  
**Integer Induction**  //第一数学归纳法  
  
to prove $\forall \, n \isin \natnums^+, \, S(n)$  
  
just to prove:  
1\.basis: 证明S(0)成立  
2\.inductive step: 当S(n)成立时，证明S(n+1)也成立 
  
**Interger Induction - Complete Induction / Strong Induction**  //第二数学归纳法/完整归纳法    
1\.basis //可以有多个basis case    
2\.inductive step  //在证明S(n+1)为真时 不仅是S(n),还有S(n-1)...S(0)都可以用于推导  
  
**Structural Induction（结构归纳法）**  
可以用递归方式定义（Recursive Definition）结构，比如自然数集就可以用归纳方式定义：  
Basis: 0是自然数  
Induction： 如果n是自然数，那么n+1也是自然数 //集合的集数/势 cardinality    

设X是递归方式定义的结构，证明$\forall X , \, S(X)$时，可用结构归纳法  
 1\.basis S(X)对基本结构成立  
 2\.inductive step 设（take）X是基于Y1,Y2...Yk递归定义的结构， 证明当S(Y1),S(Y2)...S(YK)成立时，S(X)成立    

**Mutual Induction**  
证明$\forall X , \, \operatorname{S_1}(X) \operatorname{AND} \operatorname{S_2}(X) \operatorname{AND} ... \operatorname{AND} \operatorname{S_k}(X)$  
在某些情况下 可以用归纳法对各个命题分开证明  