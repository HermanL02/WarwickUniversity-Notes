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

|![[Pasted image 20240812224721.png]]

S表: 
100001 
11代表纵向列 11->3 第四行
0000代表横向行 0000->0 第一列

P表: 
一堆数字 代表 n->n

Triple DES: More Secure than double, because meet in the middle
### AES
![[Pasted image 20240815215416.png]]

# Bitcoin
## Elliptic Curve Cryptography

