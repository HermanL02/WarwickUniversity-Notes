# Format
All questions are required. 
# Part I: Cryptograph
## Classical Crypto
### Classical Attacks
1. Ciphertext only
2. Known Plaintext
3. Choose Plaintext
4. Choose Ciphertext
### Cipher types
Shift cipher, substitution cipher, Vigenère cipher, 
Break Cipher Process: Kasiski test + the index of coincidence
## Stream Cipher
1. Stream cipher: Reuse the key; One time pad: Key length limit
2. DVD CSS Broken
## Block cipher
1. DES: **Drawing One Round**
2. Feistel Network - IMPORTANT
3. Why DES double time cannot provide 112 bits security? 
4. Drawback of DES: Key size too small. 
## Block cipher II
1. AES (No need memorize design)
2. How Confusion and Diffusion work? 
3. Why ECB insecure? Correlation. 
4. CBC: When to add pad/when to remove? 
5. Draw CBC, CFB, OFB, CRT properties, learn its recovery of error and synchronization
## Hash
1. Random Oracle(随机预言机)一个查询对应一个输出，单向的
2. Birthday Paradox 理解-> 反直觉的secure level，23个人即可有两个人生日相同的概率>50%
3. Hash Collision: Why dangerous? 
4. Draw Merkle-Damgård Construction以及证明这个! 
## MAC
1. Given AES and CBC, how to build a MAC function - 记住如何construct
2. Why H(k, m) is not secure? 
3. HMAC, timing attack是什么? 
## Key agreement
1. Understand how Diffie Hellman works. Why it is not secure for active attack? 
2. How to make Diffie Hellman secure? 
3. How Merkle Puzzle works and the complexities 
## Public Key Encryption
1. Textbook RSA encryption scheme? Key generation, encryption, decryption
2. Why textbook RSA insecure? 
## Digital signature
1. How textbook RSA signature scheme works
2. Attacks against textbook RSA
3. How Schnorr signature  scheme and Schnorr identification scheme works
# Part II: System Security
## Basics
- What is CIA traid? 
## Buffer Overflow
- Text Data BSS segment heap stack
- How EBP used to indicate memory address? 
- Steps to inject malicious code in buffer overflow
- Jumping in the malicious code: Filling NOP, spraying return address RT
- Stack Guard How? Why? 
## Race condition
- TOCTTOU attack describe
- Understand set-uid concept
- How set-uid works, eg. passwd
- Describe how to use race condition to write to passwd
## Web security - CSRF
- Same site/Cross site
- cookie used in authentication
- CSRF works? Why? 
## XSS
- Difference between CSRF and XSS
- Distinguish non-persistent/persistent XSS attacks
- How XSS self-replicate
## SQL

