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
## Basics
1. Operation Mode: 数据如何被分块处理
2. Compression: 压缩函数, 例如Feistel
3. 混淆-扩散操作: 混淆: 输入输出关系复杂; Diffusion: 每一位输入都对每一位输出有影响
### 生日悖论
意识到Hash的实际效果可能未必达到直观感受
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
如果p是一个质数，且a是一个与p互质的整数，则有a^(p-1) = 1 mod p
1. p, q质数, n =pq ;   φ(N) = (p-1) ∙ (q-1)
2. 找到随机数  e 满足 GCD (e, φ(N)) = 1
3. e * d + φ(N) * y = 1, 求d
加密: 
c = me (mod N)
解密:
m = cd (mod N)
1. Meet in the middle attack会损坏RSA Textbook
2. 我可以通过对他与其他数相乘, 来改变原数值
## 数字签名
与RSA加密类似, 私钥签名, 公钥验证
安全吗？
1. No Message Attack
2. Selected Message Attack
Schnorr signature 与 零知识证明: 完整性: 证明我知道一件事，且不需要我说出来事件本身; 健全性(Soundness): 欺骗者无法说服验证者相信陈述是正确的; 零知识性: 验证者不能学习到任何知识
# System Security
## Buffer Overflow
- Stack从高到低
- Heap从低到高
Heap变大了会导致Stack Smashing

![](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUcEWDlilEiy51i85u8QsQBVzl2h2c950cj-3h7uV1mUuExks14-Oz8Z_lYSc3V0sLq-QccYE08l-MakLr1nR5OvHQeKg6iQbThvy6UrONN1emDJLqZDCAmqlhoWdYI_WcYh7YPJ1uhKyfouueoytCKCEzINoNA=s2048?key=Hal7aljK-_3cUOO7TPPkfQ)
Text Segment: Program
Data Segment: Global Variables 
BSS: Uninitialized static/global vars
Heap: Dynamic Memory Allocation
Stack: Local vars inside functions, data related to function calls, return addr, arguments 
1. 通过填充空buffer nop来让新的address取代return address, 来指向Malicious Code; Find the offset distance between the base of the buffer and return address.
2. 已知缓冲区地址: 覆盖返回地址
Counter Measures: 
Dev: use strncpy() to check length before copy
OS: ASLR
Compiler: Stack Guard
Hardware: Non-Executable
## Race Condition
Time-Of-Check To Time-Of-Use TOCTTOU
- Between access check and use, data may have been changed. 
- A customer puts £500 on the counter to buy a product
- Cashier checks the amount and turns back to fetch the product
- While the cashier is turning back, the customer retrieves £100.
- The cashier gives the customer the product and accepts the money.
Higher Privilege -> Higher Damage
- Allow user to run a program with the program owner's privilege
- Example: passwd program

- Real UID (RUID): Identifies real owner of process
- Effective UID (EUID): Identifies privilege of a process
- Set-UID give other user RUID's privilege
Race Condition和提升权限的关系
1. 创建regular file, userA可循环运行尝试access()检查, 之后为用户open()
2. 在循环过程中symbolic link到/etc/passwd
3. 如果够巧就会access OK了, 然后刚好还没open, 就open的是新的passwd文件
Counter measure: 
1. 缩短check use windows
2. symlink禁用
3. Principles of Least Privilege: 减少后果
- Sticky Symlink Protection: To prevent creating symbolic links.
- Principles of Least Privilege:  To prevent the damages after the race is won by the attacker
## Web Security - CSRF 和 XSS
### CSRF
例子: 访问一个网站, 该网站自动发送request转账
Referer header  (browser’s help) 
Same-site cookie (browser’s help)
Secret token (the server helps itself to defend against CSRF)
### XSS
Non-Persistant:
网址里含 www.baidu.com/<script> </script> 
Persistant: 
自我复制的Samy Attack
1. 过滤 Delete Script
2. 编码 Change Coding to make script not work
3. Content Security Policy: 禁止inline script, 只允许自源Script
## SQL Injection
## Sniffing/Spoofing
Sniffer: 
NIC 网卡过滤保留TCP/DNS -> 效率高 
Spoof: 
Raw Socket来建立整个packet, 包括header
整个流程: 
PCAP API 来捕获; copy; 替换UDP数据; 源和目标调换; 发送返回; 

1. Python + Scapy
- Pros: constructing packets is very simple
- Cons: much slower than C code
2. C Program (using raw socket)
- Pros: much faster
- Cons: constructing packets is complicated
Endian: 
小Endian: 小的在前; Big Endian: 大的在前
## TCP
- TCP: provides a reliable and ordered communication channel between applications.
- UDP: lightweight protocol with lower overhead and can be used for applications that do not require reliability or communication order.
- ![Screen Clipping](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUfdCzgnAnd9_-PoMItuuocEoY_OeQVorYYpqBnd-_fqBEKW1l2F4LGy7YQc7XuhLFy-ERPy-1XogOtVd8kdWZQLzDYf7AZyPAP2UFwpz1Ch94GmSiy0pTDw2t6HD2EPnfWS7H-_UoM5uGPUVuw_IhITKMymjA=s2048?key=56yGK37EVPhBuWO29XiTJA)
- SYN Flooding Attack 导致服务器有很多open connection等待回复，占用telnet资源; **random source IP addresses**
- Counter: SYN Cookie: 每次直接返回一个Hash包含连接server的cookie, 这样就可以不存half-open connections了, If the client is an attacker, H will not reach the attacker. If the client is not an attacker, it sends H+1 in the acknowledgement field.
- ![](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUcjc0LqzFoVGtjAnrL0FyswDe8oJ0urUxFclIL1AdsCLsJg-IDtHI9zo7Q5PTMdL4PxFhFTmaa7yH9SJemjFBtMujxpiaYRmt6kaLC--x_bFS3jbXfWrg1kncVXpOnNse6veZHapAG9RMnzO8AnPacZgtgm1PI=s2048?key=56yGK37EVPhBuWO29XiTJA)
TCP Reset: 
- Retrieve the destination port (23), Source port number and sequence number.
- The next sequence number is calculated by Wireshark based on data length (choose absolute sequence number not relative one in Wireshark Preference)
TCP Hijacking Attack: 
**![](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUe2jOf891FeLrJokg6JuJekLw_RBCZfToztjd5we4bRKRgDzr5Thf8JkAkb8nJmlnqNk3gFFLNHHvTv3hV3n67WqjjrADA6vpPkQ3YaoXpPBsXBTTVHycZ4EifFeDp9Nb5W9AO-pHdeWCO_KjEAND6XEHlM_2c=s2048?key=56yGK37EVPhBuWO29XiTJA)**
Creating Reverse Shell
COUNTER: 随机source port, 随机initial sequence, Encrypting payload
## Firewall
1. User Control/ Service Control/ Direction Control
2. Accepted/Denied/Rejected(tell sender decision)
3. Three Types: Packet Filter Fire Wall, Stateful and Application/Proxy Firewall
4. Packet Filter: 注重新的连接，看header
5. Stateful: 可以只允许当前连接继续链接
6. Proxy: 中间商防火墙，例如CloudFlare
- 如何攻击防火墙
1.
- SSH Tunneling![Screen Clipping](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUf_G0p_56Wv8cyZe-EIDAJ6qPLCzN5E5dsZlFXynrBHvrus-KkZ-qDY-pLV3xYlICA7gUDvFp4PG8Y21BzwgzGR-4HnEsmTXriFWgBuo7otXtnrvDJLcwN3MRumTn1CC2atvbkTH8hgH2JwZ46F7k1Ut6cJEw=s2048?key=HM0AHIIEIP3wyRuBMVJtUQ)
- Dynamic Port Forwarding
 **SOCKS proxy on our local host.** 
SSH will send the TCP data over the tunnel to the machine “home” which will communicate with the blocked site.

- Reverse SSH Tunneling
**![](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUfEEml6Xu2YebDMA1_YI7nKhDJgVeWNBTryBxnLJbCu49TNUg86PeoF08GkT5gEBXinuN9Ht7oCAC60xJqwB61qFE2TzLCWX78gnVGI_QyA3UW4-Sr84cyJfFbPn_xiF4gopjwgyB1G3B737gp4mkUhKbMwbw=s2048?key=HM0AHIIEIP3wyRuBMVJtUQ)**
- Virtual Private Network
**- IPSec Tunneling:* / TLS SSL Tunneling

## DNS
**Denial-of-Service Attacks (DoS):** 把本地DNS服务器给DOS
Spoofing: 目的是让用户访问与他们想访问的不同的服务器
1. Local DNS poisoning: 用户发出请求后，我假装DNS服务器发送返回包
2. Remote DNS Attack: 难度大: 需要已知Source port number (16-bit random number), Transaction ID (16-bit random number); 
Kaminsky:  
**![Screen Clipping](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUcQ0rFi3xgZV03YaXOTu-BCdC7n-_CjZD54NgKyzAzYEwx6H_O2WMgf7ImPfv2blPpGmdZE0QIsDduq-MfnWqC2WM7IFrF0RyjlVdXyGnlk4QCjNfGhfHyJ2uQAdGhQcUQeVtg1DGqej9krANszOPL5qn1vu6I=s2048?key=2jp8XJK_EmXCYn2zsyRTwA)**
趁着用户Query的时候提前向DNS Server注入假的IP
3. 虚假DNS: 在回复问题的时候添加别的网站对应的IP
反向验证DNS: IP查询域名, 但是我们不能用做依据
DNS Rebinding Attack
![](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUcgM0vCL3ue4fRY43WVAJGrK6m77sQIRXI6OeIHwxTJfGR-qcuUB2B7APQ2-bHcHRXm9tvAVfBRISnyl5FF47eF-sPviZgtFneQjUloo2YctJ6Yefm7K6kJiXFUsOUSZe7AejYU58EU9H6V_QGhtwsQRoDnpg=s2048?key=2jp8XJK_EmXCYn2zsyRTwA)
Counter mesaure: 
DNSSEC 
![Screen Clipping](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUfUbfQSd-3_EAX3E-aZsmGFAsjZ6cDmSfPUo1tYtACxC7vkpDqAlKEfUXd2Pxd2LGH9dPyatNi_W5FjotgQ_spn5a5S2q7JnQuXCYv4xjtBdQnmXbTzDdJC3hybUkvLnvRuIx4z71i5qF-7IP1QPf4S37Bbng=s2048?key=2jp8XJK_EmXCYn2zsyRTwA)
DDOS  国家域名
# HSM
Tamper Evident: 就是防止篡改，篡改后能看出来，例如彩票
Tamper Resistant: 防止篡改，例如保险箱
Hack HSM: 
1. 主key由多方参与构成安全性，但是可能被忽视这个协议，因为工程师可能会访问他们本应不处理的密钥
2. 打开外壳就会获取数据，检测外壳完整性数据自动抹除，但维护人员可以获取数据 -- 组件分离, 环氧树脂密封 
3. 环氧树脂并不安全: 防篡改感应
4. 内存残留
5. 内存冰冻
6. RF射频攻击，时间攻击, 能耗攻击
## API攻击
一: 已知攻击
Host -> HSM: attacker_PAN, victim_PAN, attacker_offset
HSM -> Host: new_offset
attacker_PIN = new_offset + decimalised_PIN
Hence: victim_PIN =  decimalised_PIN + offset
			   = attacker_PIN – new_offset + offset
二. 十进制转换表攻击
0123456789ABCDEF
0123456789012345 这是正常的转换表
但是我们可以修改它
比如: 
0123456789ABCDEF
0100000000000000
这样我们就可以知道密码中是否含有1; 

三: 多个银行如何共享ATM? Visa Shared Control! 
![[Pasted image 20240824130931.png]]


# Bitcoin
## Elliptic Curve Cryptography

