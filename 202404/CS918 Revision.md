PPT = High Mark 只看PPT就能高分，想满分看之前所有内容; 每年考试Topic都不同，所以看今年的PPT; 
## RE! 必考! 
Brackets, Negations, Disjunction, Repetition, Anchors, Special Chars
例题: The set of all lowercase alphabetic strings starting with c
c[a-z]*
all strings represents dollars
我的: `\$[0-9]*.[0-9]*`
标准:`\$(\d+\.\d\d?|\d+)`
All strings that start with a lowercase letter, end with an uppercase letter, contain at least one digit
`^[a-z].*\d.*[A-Z]$`
See Photo 20240509_1017

## Text Preprocessing 
- Tokenisation
- Lemmatisation
- Stemming
### Issue in Tokenisation 
(England's capital-> England, Englands, England's)
state-of-the-art ? 4? 
Hewlett-Packard -> Hewlett Packard
Lemington Spa -> 地名，1词还是2词? 
