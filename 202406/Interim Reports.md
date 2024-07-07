
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
For text, they use keywords to find sensitive words. For picture, they compare the whole picture with the MD5 hash value with the ones they identified as politics sensitive. In recent years, WeChat also apply the filtering with Optical character recognition(OCR). 

## Current Solutions
### Virtual Private Network (VPN)
One popular practice is to use a VPN to access software outside the country to obtain end-to-end encryption. But this approach has many drawbacks.

First, the security of communication between users and VPN service providers is not necessarily guaranteed. Currently, the larger VPN providers, such as NordVPN, Express VPN, are blocked by the government, and their connection speeds are slow and very unstable. Some users choose smaller VPN providers, they usually have a smoother experience, but many providers do not have relevant service qualifications, and do not have formal business registration in any country, so the risk may be greater.

Second, VPN services are essentially in violation of relevant Chinese laws and regulations. Chinese laws and regulations stipulate that only enterprises can apply for the use of international communication channels, and individuals generally have limited requirements for application and are unlikely to be approved.

Third, the use of VPN is not convenient. If we are always connected to VPN, some software cannot be used. For example, the access speed of government affairs software, enterprise information query software and all kinds of WeChat mini programs will become very slow.
\
### E2EE Deprecated Solutions for WeChat
In the past, there are some open source solutions attempt to use web version of WeChat to intercept the messages. It avoids the complexity of reverse engineering. However, as WeChat aware of the potential use of WeChat Web version, they are forcing users to switch to WeChat Desktop version. Therefore, the web version's use becomes very limited. 
# Progress
## Windows
Our app targets to make use of the open source WeChat hook to intercept the incoming WeChat messages, and send encrypted outgoing messages. During this process, RSA will be used as the main protocol to ensure the E2EE communication. 
### Underlying Technology Stack
The underlying technology behind the WeChat injector is a sophisticated application of reverse engineering. The original author developed this tool from a publicly available GitHub repository. The process begins by using Cheat Engine to monitor the WeChat process, specifically targeting the sending of messages and setting breakpoints. This allows for the identification of the corresponding assembly code responsible for these actions. Subsequently, APIs are established to leverage this assembly code for sending and receiving messages.

Additionally, the injector exploits a vulnerability in SQLite3. SQLite3 is used to maintain compatibility, with its API designed for downward compatibility. The approach involves using the `sqlite3_close` function as an anchor to locate other functions, based on the assumption that their offsets will remain consistent. This method allows for the systematic identification and utilization of various SQLite3 functions by referencing their fixed offsets.
### General Structure
In our application, the whole application is designed following the usual MERN (MongoDB, Express, React and Node) based structure. We applied this structure with an Electron based app. The similarity between MERN stack and Electron means it is possible for a single full stack developer to create, design and build the whole process. Both of them uses Node.js as the backend and React.js as the frontend. Besides, it maintains key features as the desktop node, which means it could interact with the files to inject WeChat, create local database to save keypairs and make use of the WeChat hook, while keeping connection with the local APIs. Since our app is a security based app, it isolates the backend node.js and uses secure IPC(inter-process communication) calls to communicate between frontend and backend code to maintain the best security practice. 

Similar to MERN stack, we choose NeDB as our local database, because compare to MongoDB, it is more light weighted while keeping the NoSQL DB feature and similar command as MongoDB. 
### Back End
The backend maintains the communication between DB and utility tools including the WeChat installer (for people to easily install WeChat) and the Injection Tools (to make use of the WeChat hook to inject WeChat). It also provides the encryption, decryption and generate keypair function to the front end. 
### Front End
On the front end, tailwind CSS is used to design the scope and to perform simple animations. React is used to make the front end componentized. 
We applied React Context to continuously read the content and share the chat messages history among all React front end pages. It is also used to keep the front end state. It provides the injection page, encryption decryption page, and the chat page to the users. 
## Android
On Android side, our original plan is to integrate and inject WeChat injection tools again to our Android devices, but usually the Android devices have a more strict control over the apps. Therefore, to inject WeChat, a rooted device is required for users to use the app. However, our previous main goal is to provide a general solution for the non-tech people, but rooting devices requires the users to have a deeper understanding in Android. Therefore, we decided to make a supplementary solution for the mobile device. This solution is more likely to be a support tool to the main Windows software. 

The key idea of this app is to design a keyboard app, which allows users to save multiple keypairs, and create their own keypair. They can encrypt and decrypt the messages while sending and receiving text messages without rooting their devices. 

During the Master's degree period, it is almost impossible for a student to design an easy-to-use input method to be competitive as the main Chinese competitors like Sogou and Baidu. But recently in April 2024, the citizen lab published another article regarding the Chinese input methods, in this report, almost all the keyboards app have potential vulnerabilities.  Therefore, we had to search on the GitHub and finally chose Fcitix5 for Android as our choice. It is open source, offline, and has a wide range of users, and relatively easy to modify. 

The project is a Kotlin based software and can support java integration. 
### Code Structure
The main code structure follows the original keyboard pattern, as we want to keep its keyboard functionality as much as possible. 

We created a new set of data in shared preferences to store user private key and user public key, as well as friend public keys, so we can store the information without the information being read by third party apps. We also used the Room Database to monitor the clipboard. 

The controllers can generate keypairs, add contact public keys, and decrypt/encrypt the messages. It also communicates with the Java encryption modules. 

The front end consists the nickname input. 
## Interaction between Windows and Android Platforms

Initially, we used a conventional method to read file information and messages. This approach involved extracting the corresponding RSA key by checking for keywords in the file. However, we later switched to a unified JSON message format. JSON messages facilitate the transmission of the same information across multiple devices and languages more conveniently, avoiding compatibility issues between different languages.

We adopted the same RSA encryption method and settings to ensure that the generated RSA keys are identical. Additionally, I designed a feature that allows the RSA key generated on the mobile device to be imported into the computer. This enhances the synchronization of keys across multiple devices, ensuring that other contacts do not need to store different public keys for different platforms multiple times.

# Project Management and Future Plan

## Version Control

During this project, we extensively utilized Git as our version control tool. Git's robust branching and merging capabilities allowed for self progress checking, ensuring that code changes could be tracked, reviewed, and integrated efficiently.

## Issue Tracking

To manage and track the progress of tasks and issues, we employed GitHub Issues and Jira. These tools enabled us to create, assign, and monitor issues, facilitating a self-sprint period where tasks were planned, executed, and reviewed systematically. This approach helped in maintaining a clear overview of the project's status and ensured timely resolution of issues.

## Continuous Integration and Continuous Distribution (CI/CD)

To streamline our development process and ensure that our application was always in a deployable state, we implemented a CI/CD pipeline using GitHub Actions. This pipeline was configured to run Electron Builder, a comprehensive tool for packaging and distributing Electron applications, whenever code was pushed to the repository. This automated process ensured that our builds were consistent, reducing the likelihood of human error and speeding up the release cycle.

# Problems and Issues
During the development process, several issues can cause progress to stall. As a junior developer, encountering specific problems often leads to confusion and difficulty in finding solutions. While resources such as Stack Overflow and ChatGPT provide some assistance, they cannot fully replace the guidance of senior developers. This project’s complexity, involving the integration of front-end, back-end, and an injector, poses significant challenges. The solution of this would be better to improve myself, during the past 4-month work at Koii Network, I have learned a lot of Electron development skills . 

Another challenge is working with an unfamiliar programming language. Although I am proficient in web application development using Electron, I opted to develop a keyboard app, which necessitates the use of Java-Kotlin with Android Studio due to the inadequacy of React Native for this purpose. My limited experience with Java-Kotlin adds to the difficulty. The solution would be better learn Java and Kotlin skills from all the resources, including Stack overflow, Cainiao Tutorial and ChatGPT. 

A further complication involves handling photos. Currently, WeChat does not download photos directly to the local computer but keeps them on an intermediary server. Consequently, the received photo may not be the original one sent by the user, complicating the encryption and decryption processes. This solution is we can turn the photos to files, and WeChat usually cannot compress and modify the photo files. 

Finally, there are issues with interaction between Java/Kotlin and JavaScript. Despite both being similar languages, discrepancies arise when implementing the same RSA protocol and its configurations. While this issue has been mostly resolved by adopting a more universal package compatible with both Android and Windows applications, it remains a noteworthy challenge.
# Evaluation

