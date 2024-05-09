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
## Word Senses and Similarity 
Synonymy 是什么意思 = binary 他和similarity的关系 要记住
Relatedness measures可能的association
### Word Senses
Homonymy 同词不同意思
Polysemy 同词相近含义
Synonyms 
Antonyms
## Two Types of Similarity Algorithms
### Thesaurus-based algorithms 不需要记住所有的，但是记住如何应用，大概含义
公式 Do words PMI(word1, word2)
We don't have Thesaurus for every language. 
### Distributional algorithms
vector-space models 一样的
A/B 同意思
tackle the task tackle the news
deal with the task deal with the ...
#### Termi Context Matrix for Similarity 
Vector表，Vector更近意味着更相似
### Pointwise Mutual information

### N-gram models
过去: polysemy和synonymy的区别，举例说明
### Representing words as discrete symbols
### Word Embeddings
1. 与1 hot相反
2. 减少dimension
3. Count-based methods/Prediction-based methods
Two words are similar in meaning if their context vectors are similar
### Term Context Matrix generate Word Embeddings
### Word weighting
0509_1103 公式
### How? mesaure similarity between vectors
COSine better: Dot product和他类似 但是不需要scaling factor of vectors
### Document vectors

### Skip-gram Algorithms (Word2Vec)
Skip gram algorithms with negative sampling (SGNS)是什么? 
1. Treat the target word
这个alg的目的
### FastText
n-grams of subwords (一半的词)
Advantage: can deal with out-of-vocabulary words

Glove 
Count based 
Matrix based
他怎么做到的? 
图0509_1110
有了concurrence matrix

### Bias和Fairness
He works as a -------------> Doctor最高 Receptionist低. 
She 默认 ----------> Nurse最高 --> engineer最低 
还是用entrisic and intrinic来evaluate
过去: how do we compute the similarity between two word vectors using embeddings? 


## Text Classification
非常重要, 对于exam来讲! 
- Binary: 
- Multi-class
- Overfitting? 
你必须会matrix
Evaluation of binary classification 0509_1122 1123
Precision and Recall
`F = 2 *(precision*recall)/(precision+recall)`
多类别classification
F1 score 
Macro average /Micro average 怎么算 公式没拍下来! 
从SDQC表获取Precision and Recall 和Macro Micro 计算题
过去: What is overfitting? 
not generalize （关键词）
过去: What is difference microavg and macroavg? 
Micro 无需计算每个分类 Macro 计算每个分类
POS targeting
Markov Chain 
什么是transition probability./emission probability 画一些图来解释MD VB NN; 什么是Markov assumption
例子 __1131
HMM 是什么
我们如何找到best tag sequence emission transition （需要具体的公式) 
Viterbi Algorithm是什么: 如何用就行，不需要如何apply或者具体细节
Entropy 为什么重要-> Maxium Entropy Models （需要具体看) 
MEMM(需要what it is why it is happending)
Conditional Random Field ()
过去: What is Part of speech? Why it is a sequential problem? 
POS: 例题2: _1138
不需要Context Free Grammars 记住sequence，但是要会用
Grammars and Parsing
两种syntactical Structures
1. Constitancy
Parsing
Lexicalisation Parsing
PCFG是什么
