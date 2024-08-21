# Intro
## Terms
Vulnerability: Weakness in the system that could be exploited to cause harm
Threat: A set of circumstances that has the potential to cause harm
CIA: Confidentiality, Integrity and Availability
Other: 
Authentication: Password/Token/Biometrics; 
Non-repudiation: 不可抵赖性


# Crypto
## Classical
### Four General Types of Attack
- Ciphertext-only
- Known-plaintext
- Chosen-plaintext
- Chosen-ciphertext
To store all 256-bit Keys 2264 bits

### Shannon Principle:  Confusion and Diffusion

- Confusion: 模糊Plaintext/Ciphertext之间的关系
- Diffusion: 破坏规律, 例如字母出现频率等
### Shift Cipher
#### Caesar Cipher
向右移动3位
#### ROT13
向右移动13位, 对称性: 解密加密相同方式

### Substitution Cipher
根据字母频率可以破译

### Vigenère cipher
原因: 以单词作为key
破解: 查找重复词来判断位移量 -> Index of Coincidence

## Stream Ciphers
目的: 为了让One Time Pad Practical，用短Key生成长的Key Stream
种类: Vigenère **cipher**

### One Time Pad
Unbreakable
### Base: Probability
Joint Probability
![[Pasted image 20240819215751.png]]
Conditional Probability
![[Pasted image 20240819215716.png]]
Bayes Theorem
![[Pasted image 20240812214746.png]]
Perfect Accuracy
![[Pasted image 20240819215927.png]]
### 除了Vaigenere Cipher以外的另外一种Recurrence Cipher
![[Pasted image 20240812215646.png]]
例如k5 = (k1+k2) mod 2
### LFSR 硬件Recurrance
比如异或1，2得到4，同时向左移位
![[Pasted image 20240819221327.png]]
### Attack
- Two Time Pad
	C1 异或 C2 = M1 异或 M2 => {m1, m2}
- Integrity: 修改密文
- CSS光盘: 
17bit LFSR尝试得到20bytes output, 在output中减去20bytes，然后如果和25 bit的LFSR相同，则找到了密钥

## Block Cipher
### DES 
正常是2的168位加密程度，但是实际man in the middle只需要2的112位加密
### Feistel Network
- 每一轮（第 ii 轮），使用一个密钥K和右半部分R0作为输入，进入一个函数 F(Ki, Ri) 该函数的输出与左半部分 Li 进行异或运算
- 计算得出新的右半部分 Ri 
  原来的右半部分 Ri 则直接作为新的左半部分 Li
  最后一轮直接下去, 则不需要交换了

|![[Pasted image 20240812224721.png]]

S表: 
100001 
11代表纵向列 11->3 第四行
0000代表横向行 0000->0 第一列

P表: 
一堆数字 代表 n->n

Triple DES: 即使两个key相同，也可以产生更高security
### AES
Substitution Permutation Network
![[Pasted image 20240815215416.png]]
Input->Key->Sub->Permu->Key->Sub->Permu->...
SubBytes（S表字节替换）、ShiftRows（行移位）、MixColumns（列混淆）和AddRoundKey（轮密钥加）

概念: 有限域Finite Field
**逆元计算**：有限域的一个重要性质是，每个非零元素都有一个唯一的乘法逆元，这在密码学中至关重要。例如，S盒的构造就是通过对有限域GF(2^8)中每个元素求逆来实现的。

### AES和DES区别
- S-box非随机
- 固定域
- S-box非硬编码
- It allows very compact software implementation (say on smartcards)
- Flexible trade-off between the code size and the performance

- Electronic code book mode (ECB) -> Same input same output -> Pattern
- Cipher Block Chaining mode (CBC) -> 随机IV, 连续Block都会被影响，整block丢了可以被恢复，Encryption是线性的，会加padding，如果无padding会加一整块; 
Padding Oracle 攻击: 修改密文的最后padding发送给服务器来判断填充是否无效
- Cipher feedback mode (CFB) -> Change Block Cipher to Stream Cipher
- Output feedback mode (OFB) -> Stream Cipher, 加解密操作相同，可以平行解密
- Counter mode (CRT) -> Stream Cipher, 加解密相同流程，可以平行加解密
## Hash
### 生日悖论
意识到Hash很难
### Merkle
- Merkle-Damgård构造是一种迭代的哈希函数构造方法，通过将消息分块处理并结合初始向量（IV）生成最终的哈希值。
- 这种构造方法的关键在于使用一个压缩函数`h`，将消息块与前一个中间哈希值组合起来，生成新的中间哈希值，直到处理完所有的消息块，最后生成最终的哈希值`H(m)`。
应用: Sha-256，签名，密码
Attack: Dictionary Attack
## MAC - Integrity

 **-  MAC I = (S, V) defined over (K,M,T)**
 S: Generate Tag; V: Verify Tag
 K: Key; M: Message; T: Tag
-  S(k,m) outputs t in T
- V(k,m,t) outputs “Yes” or “No”
用例: 用户电脑中毒，电脑自动判断文件完整性来恢复
- 构建方法: Block MAC-> CBC MAC或者Hash MAC, HMAC
- CBC: FIXED IV; 
- Hash: 长度扩展攻击，为他多添加一段东西，生成新MAC，会篡改原本的MAC吗
- **H(k1, H(k2, m)) where k1 and k2 are two different keys**
- **HMAC(k,m) = H( k⊕opad  ll  H( k⊕ipad ll m ) )**
- Hash攻击2: 时间比较攻击: 
  Byte by Byte Comparison, 在第一位不正确时返回, 通过时间可判断是否正确
Tampor Attack
- **初始通信**：
    - 假设Bob要向服务器发送一个加密的消息，这个消息可能是“dest=80 data”，其中`dest=80`指的是目标端口80（通常是HTTP端口），`data`是实际的传输数据。
    - 使用CBC模式加密时，Bob会生成一个随机的初始向量（IV），然后将这个消息和IV一起发送给服务器。
- **攻击者截获并修改消息**：
    - 攻击者k截获了这个加密消息和IV。
    - k将消息中的初始向量IV改为IV'，并将消息中的`dest=80`改为`dest=25`（假设端口25是Bob的邮件服务器端口，用于发送电子邮件）。
- **服务器解密消息**：
    - 服务器收到这个经过修改的消息时，会用IV'和Bob的密钥来解密消息。因为CBC模式是逐块解密的，而攻击者只修改了IV，所以解密后的数据看起来依然是有效的。
- **消息被发送到错误的目的地**：
    - 解密后，服务器看到的消息是“dest=25 data”，这表示该消息应该被发送到端口25（可能是Bob的邮件服务器）。
    - 服务器于是将“data”部分发送到Bob的邮件服务器端口（端口25），而不是原来预期的端口80。
- **攻击者获取信息**：
    - 由于这个消息本质上是Bob预期发送给端口80的数据，但现在被发送到端口25，攻击者k可以通过监听端口25来截获这个解密后的数据。
    - 这样，攻击者就获取到了Bob发送的“data”内容。
## Key 交换
### Merkle交换
A生成2^32 puzzle 每个puzzle都包含两个部分：128位的 xi 和 128位的 mi。, B收到2^32 puzzle从中选1个解决拿到ki并返回, 监听者需要花费2^32次方时间才可以evedrop 

### Diffie-Hellman
A=g^a mod p
B=g^b mod p
交换 A B
A的公钥 s = B^a mod p
B的公钥 s = A^b mod p
指数级但无integrity, 容易遭受Man in the Middle Attack
怎么办? 1. Public Key...SSL, TLS... 2. Password, **J-PAKE** **SPEKE** 

交换的基础是内容是random的，但是内容不是random导致问题
## 公钥加密
G, E, D, 随机化, 加密, 解密

# Bitcoin
## Elliptic Curve Cryptography

