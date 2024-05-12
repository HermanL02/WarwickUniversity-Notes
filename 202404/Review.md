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

# 2
