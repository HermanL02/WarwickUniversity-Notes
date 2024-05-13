# 1
### a
i: Each of X corresponds to Y 
ii: X and Y relationship is both Injection and Surjection 
iii: `P(N x (N* N))`
### b
i: 
1. No relation between each printer and the options
2. maxnum should be at least 1. 
ii: 
MACHINE Access
SETS USER; PRINTER; OPTION
CONSTANTS options, maxnum
CONSTRAINTS options: PRINTER <-> OPTION, maxnum:NAT1, forall p.(p ∈ PRINTER, card(options[{p}])<= maxnum)
iii. 
MACHINE Access
SETS USER; PRINTER; OPTION
CONSTANTS options, maxnum
CONSTRAINTS options: PRINTER <-> OPTION, maxnum:NAT1, forall p.(p ∈ PRINTER, card(options[{p}])<= maxnum)
VARIABLES user_access
INVARIANT user_access ∈ USER ↔ PRINTER
INITIALISATION user_access := ∅
### c
i. 
```
add(pp) = 
PRE pp ∈ USER*PRINTER
THEN user_access <- pp
END
```
ii. 
```
remove(uu) = 
PRE uu ∈ USER
THEN 
user_access = {pp| pp∈user_access∧ dom(pp) ≠ uu}
END
```
iii. 
```
unify(uu1,uu2) = 
PRE uu1 ∈ USER and uu2 ∈ USER and uu1 ≠ uu2
THEN 
user_access := user_access ∪ ({user1} × user_access[{user2}]) ∪ ({user2} × user_access[{user1}])
END
```
iv. 
```
pp <- findpp(oo) = 
PRE  oo ∈ OPTION and oo ∈ dom(user_access)
THEN pp := {ppp| ppp∈PRINTER and oo ∈ options[{ppp}] }
END
```
v. 
```
pp <- findpermited(oo, uu) = 
PRE  oo ∈ OPTION and oo ∈ dom(user_access) and uu ∈ USER and uu dom(user_access)
THEN pp := {ppp| ppp∈PRINTER and oo ∈ options[{ppp}] and uu ∈ user_access[{ppp}]}
END
```
vi. 
```
rr <- average_options = 
ANY avg 
WHERE avg ∈ ℚ ∧ card(PRINTER) > 0 ∧ avg = (Σ(p).(p ∈ PRINTER | card(options[{p}]))) / card(PRINTER) 
THEN rr := avg
END
```
2. a) a conjunction means and, which requires all the options to be true, but implication can in some extent can be False-> True, which does not meet the requirement. Ex. if I want to have aa = 1 and bb = 1, if I use a->b, it could implies a condition which aa!=1 and bb=1, which may also pass the pre condtion. 
	b) 
5. a) B0 is the “concrete” subset of the B language. Int, boolean, sets, array/record of them. 
b)  
```
MACHINE Modules
SETS STUDENT, MODULE
VARIABLES modchoice
INVARIANT modchoice ∈ STUDENT<-> MODULE
INITIALIZATION modchoice := ∅
OPERATIONS 
add_student_module(std, mod) = 
PRE 
std ∈ STUDENT ∧ mod ∈ MODULE ∧ card(modchoice[{std}]) < MAX_CHOICE ∧ std ∉ dom(modchoice) ∨ (std |-> mod) ∉ modchoice THEN 
modchoice := modchoice ∪ {std |-> mod} 
END; 
mod <-- has_module(std, mod) = 
PRE std ∈ STUDENT ∧ mod ∈ MODULE 
THEN 
(std |-> mod) ∈ modchoice 
END 
```
   c) Errors Set