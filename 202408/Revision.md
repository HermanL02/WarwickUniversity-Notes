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
- Output feedback mode (OFB) -> 加解密操作相同
- Counter mode (CRT) -> 

# Bitcoin
## Elliptic Curve Cryptography

