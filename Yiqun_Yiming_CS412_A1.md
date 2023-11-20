
# Authors
- Yiming Kao (yiming.kao@warwick.ac.uk)
- Herman Liang 5526872 (yiqun.liang@warwick.ac.uk)
# Question#1
## Part A.
The question tells us that only one of the statement is true. 
First, we can use truth tables to  represent the relations of the two statements $King \rightarrow Ace$ and $¬King \rightarrow Ace$, then to determine where the results are controvertial. 

| King | Not King| Ace | $King \rightarrow Ace$ | $¬King \rightarrow Ace$ |
|---|---|---|-------|-------|
| T |F  | T | T     | T     |
| T |F  | F | F     | T     |
| F |T  | T | T     | T     |
| F |T  | F | T     | F     |

By examining rows 2 and 4， where $King \rightarrow Ace$ and $¬King \rightarrow Ace$ have different results, we observe that while the condition for the King varies, the condition for the Ace remains consistent. This confirms that the statement **'There is not an ace in the hand.'** is necessarily to follow. 

## Part B.
- Simplification
$[nn, ii := nn + ss(ii), ii + 1](nn = \sum xx \cdot (xx \in 1 . . ii − 1 | ss(xx )))$
Therefore, we can separate the multi-assignment as $nn = nn + ss(ii)$ and $ii = ii + 1$
By substituting, we can get $nn+ss(ii) = \sum xx \cdot (xx \in 1..ii|ss(xx))$
- Where might this sort of situation arise?
This equation represents loop/iteration. If we investigate deeper, it may also implies the Loop invariant. Through the definition from [Wikipedia](https://en.wikipedia.org/wiki/Loop_invariant#:~:text=In%20computer%20science%2C%20a%20loop,the%20effect%20of%20a%20loop.), a loop invariant is a property of a program loop that is true before (and after) each iteration. It can help us to make sure that the algorithms produces the correct results. 


## Part C.
In this question, supposing if we have already corrected the initialization part, we don't have to change the addmark function. This also applies to the reverse condition - supposing if we have already changed addmark function part correctly, we don't have to change the initialization part. 
- Initialisation Correctness:
    - Requirement: The initialization must satisfy the invariant.
        - ==Achieved Part==
            - The operation creates an empty set.
        - ==Error/Missing Part==
            - The initialization should also should create empty relations from 0 to mmax, and give them a value of 0. 
    - Correction: Shown below

        
        -   ```
                 INITIALISATION record := %ii.(ii ∈ 0..mmax | 0)
            ```
    - Proof: INITIALISATION record := λi.(i ∈ 0..mmax | 0) satisfies the invariant, and avoids the operation to read a null value. 
- Operation Correctness:
    - Requirement: For every operation, they must satisfy the pre-condition and the invariant. 
        - ==Achieved Part==
            - The operation assumes mm is natural number
        - ==Error/Missing Part==
            - The operation should have a pre-condition that mm is between 0 to mmax. 
            - The operation should consider if mm doesn't exist in the record, the statement record(mm) := record(mm)+1 will fail. 
    - Correction: Shown below

        
        -   ```
            addmark(mm) =
                PRE mm ∈ 0..mmax THEN
                    IF mm ∈ dom(record) THEN
                        record(mm) := record(mm) + 1
                    ELSE
                        record := record ∪ {mm |-> 1}
                    END
                END
            ```
    - Proof: 
        - The pre-condition of mm now within the range
        - The if-else condition now handled the case that the mm is in the record. 
        
## Part D.
1. Logic: Supposing we need to check whether 'tt' is a sub sequence of 'ss', and we know that if 'tt' exists, tt's starting index should between the beginning of 'ss' to the end of ss minus the size of 'tt'. Then from the starting index, we can find a jj Therefore, we need to use non-deterministic ANY to find whether this ii exists. 
    ```
    result <-- is_subsequence(ss, tt) = 
        PRE  ss: seq(NAT) ∧ tt:seq(NAT)
        THEN
        ANY ii,jj WHERE
            ii ∈ 1..(size(ss) - size(tt) + 1)&  jj:NAT1 &  ss\|/(ii)/|\(jj) = tt
        THEN
            result := TRUE
        END
    END  
    ```
2. Logic: Search for a new sequence, named st, whose elements range from 1 to card(ss). The elements of st come from the union of all indices in ss. It is specified that the length of st is the same as card(tt), and st is ordered. st represents the mapping from indices in tt to indices in ss. Finally, for all i, it holds that ss(st(i)) = tt(i). If such an st exists, the result is true.

```
OPERATIONS  
    result <-- is_general_subsequence(ss,tt) =   
     PRE
      ss : seq(NAT) & tt : seq(NAT)
     THEN
      ANY st,ii WHERE
        st : seq(NAT) & //st is a sequence
        ii : 1..card(tt) & //card(st) is the same as card(tt)
        st(ii) ∈ 1..card(ss) & //The elements of st come from 1..card(ss)
        !(ii,jj).(ii:1..card(st) & jj:1..card(st) & ii <= jj=> st(ii)<= st(jj)) & //Sort st in ascending order
        ss(st(ii)) = tt(ii)//st represents the mapping from indices in tt to indices in ss
      THEN
        result := TRUE
      END
    END
END