# Introduction
In today's digital era, instant messaging platforms have become integral to daily communication. To ensure the communication security, many users prefer to use the secured communication apps such as WhatsApp, which provides an end-to-end encryption feature. 

However, in People's Republic of China(PRC), these secure apps are not accessible due to the government applied internet restrictions. Instead, in the Chinese market, among all these platforms, WeChat stands out with over 1 billion daily active users, making it a dominant force in the messaging area. However, compare to the competitors on the global market, we found neither of the Chinese apps provides a End-to-End Encryption(E2EE) feature nor seen security and communication safety as their priority. 

Therefore, we want to introduce an End-to-End Encryption solution for WeChat with main focus on Windows and Android platforms, which may potentially benefits people who can only access to mainland chat applications and the people who need to keep contact with mainland friends. We give it a name, Libre Chat. 
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
The underlying technology behind the WeChat injector is a sophisticated application of reverse engineering. The original author developed this tool from a publicly available GitHub repository. The process begins by using Cheat Engine to monitor the WeChat process, specifically targeting the sending of messages and setting breakpoints. This allows for the identification of the corresponding assembly code responsible for these actions. Subsequently, APIs are established to leverage this assembly code for sending and receiving messages.

Additionally, the injector exploits a vulnerability in SQLite3. SQLite3 is used to maintain compatibility, with its API designed for downward compatibility. The approach involves using the `sqlite3_close` function as an anchor to locate other functions, based on the assumption that their offsets will remain consistent. This method allows for the systematic identification and utilization of various SQLite3 functions by referencing their fixed offsets.
### General Structure
In our application, the whole application is designed following the usual MERN (MongoDB, Express, React and Node) based structure. We applied this structure with an Electron based app. The similarity between MERN stack and Electron means it is possible for a single full stack developer to create, design and build the whole process. Both of them uses Node.js as the backend and React.js as the frontend. Besides, it maintains key features as the desktop node, which means it could interact with the files to inject WeChat, create local database to save keypairs and make use of the WeChat hook, while keeping connection with the local APIs. Since our app is a security based app, it isolates the backend node.js and uses secure IPC(inter-process communication) calls to communicate between frontend and backend code to maintain the best security practice. 

Similar to MERN stack, we choose NeDB as our local database, because compare to MongoDB, it is more light weighted while keeping the NoSQL DB feature and similar command as MongoDB. 
### Back End
The backend maintains the communication between DB and utility tools including the WeChat installer (for people to easily install WeChat) and the Injection Tools (to make use of the WeChat hook to inject WeChat). It also provides the encryption, decryption and generate keypair function to the front end. 
### Front End
It uses a React Context to continuously read the content and share the chat history among all React front end pages. It provides the injection page, encryption decryption page, and the chat page to the users. 
## Android
On Android side, our original plan is to integrate and inject WeChat injection tools again to our Android devices, but usually the Android devices have a more strict control over the apps. Therefore, to inject WeChat, a rooted device is required for users to use the app. However, our previous main goal is to provide a general solution for the non-tech people, but rooting devices requires the users to have a deeper understanding in Android. Therefore, we decided to make a sublementry solution for the mobile device. This solution is more likely to be a support tool to the main  during the Master's degree period, it is almost impossible for a student to design a easy to use input method for 
### Code Structure

### Details


# Project Management and Future Plan


# Evaluation

