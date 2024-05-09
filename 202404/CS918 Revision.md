PPT = High Mark 只看PPT就能高分，想满分看之前所有内容; 每年考试Topic都不同，所以看今年的PPT; 但是PPT不会有原题; 
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
答题技巧: LEE; List Explain and Example

### Tokenization in Chinese 
预处理不同
例题: What is the difference between lemmatization and stemming? 
Lemmatization: is, are -> be
stemming: 不一定是一个真实的单词例如living -> liv
## N-grams
### Statistical Language Model
I want to -> high
want I to -> low
### MLE公式
P(W1|Wi-1) = count(W_(i-1), Wi)/count(w_(i-1))
## Markov Assumption
Probability
You might be asked to compute the probabilities of them
P(want|I)
## Practical Solution
如果过小
用Log space来找到概率 
Sum instead of multiplication
## Smoothing
1. Laplace
2. Interpolation
3. Good turing
4. Kneser-Ney 
5. (四个其中一个会考，所以所有的都要熟悉，explanation and problems, 过去也考过几道，这个回去看看PPT关于这几个, listing provide examples, 同时也可能有解决问题)
## Evaluation
1. Extrinsic or in-vivo evaluation
2. Intrinsic or in-vitro evaluation
### in-vivo
LM1 LM2 ...
### in-vitro 更复杂
#### Perplexity? 
你对于下一个word的prediction是否准确/困难? 
The Shannon Game: How well can we predict the next word? 
1. unseen test set
2. maximise P(sentence) -> Low Perplexity
PP(W) = 公式: 0509_1041
Chain rule 0509_1042
之前: what is smoothing and why do we use it in language modelling
答案: 0509_1043 
之前: Describe one way of performing extrinsic evaluation of language modelse, and another way of performing intrinsic evaluation? What is a disadvantage of each of these evaluation techniques? 
答案: 0509_1044
## Sentence probability
1. 计算probability问题 0509_1046
## Word Se