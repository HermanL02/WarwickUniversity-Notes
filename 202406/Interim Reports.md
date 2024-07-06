# Introduction
In today's digital era, instant messaging platforms have become integral to daily communication. To ensure the communication security, many users prefer to use the secured communication apps such as WhatsApp, which provides an end-to-end encryption feature. 

However, in People's Republic of China(PRC), these secure apps are not accessible due to the government applied internet restrictions. Instead, in the Chinese market, among all these platforms, WeChat stands out with over 1 billion daily active users, making it a dominant force in the messaging area. However, compare to the competitors on the global market, we found neither of the Chinese apps provides a End-to-End Encryption(E2EE) feature nor seen security and communication safety as their priority. 

Therefore, we want to introduce an End-to-End Encryption solution for WeChat with main focus on Windows and Android platforms, which may potentially benefits people who can only access to mainland chat applications and the people who need to keep contact with mainland friends. 
# Background and Research
## E2EE Measures from a Global Perspective
There are four properties are used to ensure the messaging is secure, which are confidentiality, integrity, authentication and non-repudiation. [PDF Ref1] There are many encryption protocols are designed to fulfil the these properties, such as Signal protocol and the RSA protocol. 

iMessage, WhatsApp and Zoom provides a default E2EE or provides a E2EE option. iMessage uses PQ3 protocol, WhatsApp and Signal uses Signal protocol. Telegram uses MTProto Protocol. Proton Mail uses RSA protocol. [PDF Ref1]

We can generally consider that E2EE is widely used outside internet restricted area. 
## Current WeChat Encryption Measures
According to the official website of WeChat help center, WeChat uses TLS encryption to secure your data as it moves to and from the servers. For the static data, it uses 256 digits AES encryption. However, during this process, the encryption key is controlled by service provider, Tencent, which means it has a potential threat that Tencent has access to your information and conversation. [https://help.wechat.com/cgi-bin/micromsg-bin/oshelpcenter?opcode=2&plat=1&lang=en&id=1208117b2mai1410243yyQFZ&Channel=helpcenter]

## WeChat Scandal
Above, we talked about the potential technical possibility of WeChat technology. In fact, there are already reports regarding the block and filter of messages of WeChat. It also applies the account ban on sensitive politic messages. 
According to Citizen Lab of the University of Toronto, [https://citizenlab.ca/2020/05/wechat-surveillance-explained/] if a message is censored, it will not notify either the sender and the recipient. For example, in this context example, a user tries to send a sensitive word Dharma Wheel, it will be shown as 'sent' on sender's side and will not be shown on recipient side. 
For text, they use keywords to find sensitive words. For picture, they compare the whole picture with the MD5 hash value 



# Progress
## Windows

### Underlying Technology Stack
The underlying technology stake would be the WeChat injector. The idea comes from the GitHub repository. It supports the injection of WeChat through IDA, which is a tool could directly read the source code of WeChat. 

### General Structure
### Front End
### Back End

 
## Android
### Code Structure
### Details


# Project Management and Future Plan


# Evaluation

