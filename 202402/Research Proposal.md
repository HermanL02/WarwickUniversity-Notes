## Motivation
## Background
Nowadays, the balance between convenient communication and privacy has become a pivotal concern. In an era that digital communication is everywhere, the convenience of keeping communication with others seems to be granted. However, this convenience brings a strict privacy issue, because most governments and enterprises are seeking or having the ability to monitor, collect and analyse much personal communication data. The global discussion about the monitoring of chatting tools has never stopped. 

Many countries in the world take terrorist, crime and national security threats as the reason to restrict encryption attempts, including End-to-End Encryption (E2EE) technologies. E2EE is a safe communication method, which can prevent third party to retrieve the data when transmitting the data from one terminal or device to another terminal or device, which means all other external entities including the government, telecom providers, Internet providers, and even the service providers themselves does not have access to the messages. 

Although E2EE provides privacy advantages, there is resistance with implementations. Some governments believe that E2EE technologies make the criminal's communications cannot be censored and monitored. Many countries are attempting to legislative compel of tech companies that provide E2EE services. These actions result a serious discussion between privacy and the possibility of misuse of monitoring rights, shows the hardness of balancing security and protect personal information. 

China is always in the forefront of monitoring chat communications, implementing strict regulations and use advanced technologies to monitor and censor online activities. The Chinese government is trying to monitor public and personal digital communications and filter anything political sensitive or harmful to national benefits. In this situation, the use of E2EE causes a challenge of government's control and monitoring personal chats. Therefore, the real E2EE apps are facing a great barrier to pass the Chinese government's review. This stance is in line with broader Internet governance strategies in China, including the Great Firewall, which blocks access to many foreign websites and services, including popular E2EE-enabled applications like WhatsApp and Facebook Messenger. Also, in some cases, the police officer would stop you on the street to see if you are using some illegal apps, like Telegram. 

One notable example is WeChat, China's most popular messaging app, which offers an array of services from messaging to financial transactions. However, its convenience comes at a cost: significant monitoring and data collection practices that raise privacy concerns. WeChat's approach to user data is emblematic of broader trends in digital surveillance and data management within China. 

To circumvent these restrictions, some users turn to Virtual Private Networks (VPNs), which can provide a way to access blocked services by encrypting the user's Internet traffic and routing it through a server located outside of China. Nevertheless, the use of VPNs in China is fraught with challenges. The legal status of VPNs is ambiguous and potentially illegal if not government-approved, making their use a risky endeavor. Moreover, the Chinese government has been known to target large VPN providers, leading to unstable connections and further diminishing the reliability of this workaround. Smaller VPN providers, on the other hand, may offer less security and are generally considered unsafe due to their lack of robust infrastructure and potential vulnerability to surveillance and data breaches.

## Ideas
The proposed solution involves developing mechanisms to enable easy established legal, stable E2EE for users within restrictive digital environments using non-E2EE popular app, WeChat, without connecting to outside Chinese servers and without using VPNs. 
### Methodology
For the Windows operating system, our strategy encompasses utilizing a WeChat hook to employ reverse engineering techniques. This method aims to intercept messages from the WeChat application, extracting them for E2EE processing, and then forwarding these encrypted messages to a local port. Concurrently, this hook is designed to receive encrypted messages through a local API, decrypt them, and then display them within our application. Also, the user could input plain text in our software, and then the message will be forwarded to another port. Then WeChat hook could send the message to the contact through WeChat. 

On the Android platform, our approach is based on leveraging the [fcitx5-android](https://github.com/fcitx5-android/fcitx5-android) application, which boasts significant community support. This input method, renowned for its reliance on local dictionaries and regular updates, guarantees that user inputs are not transmitted to third-party entities. This framework provides a secure foundation for integrating E2EE functionalities. 

Based on the application, we want to implement a textbox within the input Android keyboard, that could receive the user input, when user click on send on keyboard, it then will send the encrypted message to the designated user. The input method also monitors  the clipboard, to decrypt the copied messages. 
### Function design
The cornerstone of our E2EE implementation is the selection of an encryption protocol conducive to online key exchanges. Initially, we propose the adoption of the RSA encryption protocol, renowned for its security and ease of key management. This protocol is used by iMessage, which is an Advanced protocol. We also need to explore more protocols. 

Integrating three different cryptographic protocols—RSA, J-PAKE, and the Signal Protocol—into our system is a strategic decision aimed at leveraging the unique strengths and security features of each to provide a comprehensive, robust, and flexible encryption framework. Here's why incorporating each of these protocols is beneficial:
### RSA (Rivest-Shamir-Adleman)

**Versatility and Trust**: RSA is one of the most widely used public-key cryptosystems, trusted for secure data transmission across the internet. Its versatility in encrypting small blocks of data, like keys or digital signatures, makes it a valuable component of a multi-protocol strategy.

**Established Security Foundation**: RSA provides a solid foundation for secure communications, based on the mathematical challenge of factoring large prime numbers. This long-established security basis is crucial for certain aspects of our system, such as initial key exchanges or digital signatures, where the proven reliability of RSA can be particularly advantageous.

RSA is going to provide basic cryptographies in our system. 

##### J-Pake
**Zero-Knowledge Password Proof**: J-PAKE enables two parties to establish a secure cryptographic key based on a shared password without ever transmitting the password or its hash over the network. This protocol offers a secure way to authenticate users in a manner that minimizes the risk of password interception or brute force attacks, enhancing the overall security of the system.

**Mitigating Man-in-the-Middle Attacks**: By ensuring that the password itself is never exposed and that the key exchange process is secure even in the presence of potential eavesdroppers, J-PAKE adds an important layer of security against man-in-the-middle (MitM) attacks, complementing the other protocols in our system.
##### Signal
**Forward Secrecy and Post-Quantum Security**: The Signal Protocol is designed to offer forward secrecy, ensuring that the compromise of one set of keys does not compromise past or future communications. This is a critical feature for maintaining the confidentiality of communications over time, even if a key is somehow compromised.

**Modern, Robust Encryption**: The Signal Protocol employs a combination of cryptographic techniques, including the Double Ratchet Algorithm, prekeys, and a triple Diffie-Hellman handshake. This modern approach to encryption is highly effective at securing end-to-end communications, making it a key part of our system's encryption framework.

The application should allow users to exchange public keys by direct sending messages. The basic function is that it can encrypt and also decrypt the message. 

Supposing there are two people, A and B, are trying to do the encrypted communication using this app. User A should be able to retrieve a WeChat message and decrypt it using A's private key and also should send a WeChat message that encrypt it using B's public key. 

By integrating RSA, J-PAKE, and the Signal Protocol, our system is designed to leverage the combined strengths of these protocols to address a wide range of security requirements and threats. This multi-protocol approach allows us to:

- **Ensure versatile and trusted encryption** for different aspects of the communication process.
- **Enhance user authentication** and mitigate specific attack vectors, such as MitM attacks.
- **Provide robust end-to-end encryption** with forward secrecy, protecting the integrity and confidentiality of messages over time.
- **Prepare for future security challenges**, including the advent of quantum computing, by incorporating protocols that can be adapted to use post-quantum cryptographic algorithms.

In summary, the choice to incorporate these three cryptographic protocols into our system reflects a comprehensive strategy to maximize security, flexibility, and future-proofing, ensuring that our system can protect users' communications against a wide array of potential threats.


## Target customers

## Target
We want to make our project scalable. 

## Deliverable and work plan
### Deliverables 
The app will mainly focus on Windows and Android phones, because my current develop environment is Windows and Android. I don't have MacOS and iPhone devices. If it is possible, we will introduce our app on more 

On Windows, we want to use WeChat hook to achieve direct chat using our app, through WeChat platform. (We will introduce details later.)  The app will be build with Electron Framework, with React.js as front end and Node.js as backend. The app will rely on IPC communication. 

On Android, due to the limitation of retrieving root privilege on Android devices, we decided to extend the current keyboard app to add another plugin using Kotlin. 

We will deploy a server using Node.js to create APIs for users to upload their public key with their WeChat unique ID and retrieve others public key using WeChat unique ID. However, we want to make sure when the server is blocked or is down, the app is still usable. 
### Work plan
The development of our end-to-end encryption (E2EE) solution for WeChat on Windows and Android platforms will adopt an agile methodology, specifically the Scrum framework, to ensure flexibility, rapid iteration, and continuous feedback throughout the project lifecycle. Project management and task tracking will be facilitated through Jira, allowing for clear visibility of progress, assignment of tasks, and collaboration among team members. The overall development timeline is estimated at approximately two months, with distinct phases allocated to the Windows and Android platforms.
#### Development Plan Overview
#### Month 1: Windows Application Development

The first month is dedicated to the design and development of the Windows application. This phase is organized into four key stages:

1. **Initial Learning and Familiarization:** Team members will acclimate to the development languages and tools relevant to the Windows platform, ensuring a strong foundation for subsequent phases.
2. **Backend Development:** Focus will shift to backend coding, particularly establishing connections to WeChat and integrating WeChat hooks for message interception and handling.
3. **Frontend Development:** The development of user interfaces (UI) aims to enhance user experience, making the application intuitive and accessible.
4. **Additional Functionalities:** Final adjustments and the incorporation of extra features to enrich the application's capabilities.

Each stage is expected to span three to four days, with progress meticulously documented and managed through our [Jira project board](https://hermanyiqunliang.atlassian.net/jira/software/projects/YIQ/boards/2?atlOrigin=eyJpIjoiZThkMmIyOWI5YzUxNDQ2NjhhNWI1ODAxZWMyMDljOGUiLCJwIjoiaiJ9). We are currently in the fourth and final phase of the Windows application development.

#### Month 2: Android Application Development

The subsequent month will be allocated to developing the Android application. The phases mirror those of the Windows development, with adaptations to accommodate the Android platform:

1. **Learning and Adaptation:** Given the Android application's reliance on Kotlin and its unique app structure, additional time will be allocated for the team to familiarize themselves with Kotlin programming and the existing keyboard app framework.
2. **Backend Development:** Similar to the Windows phase, focusing on integrating E2EE functionalities within the app's existing structure.
3. **Frontend and UI/UX Development:** Emphasis will be placed on creating a user-friendly interface that aligns with Android usability standards.
4. **Integration and Enhancement:** Incorporating additional security protocols and ensuring the application's stability and reliability.

Given the complexities associated with Android development, particularly the need to integrate with the fcitx5-android keyboard app, each phase is expected to take approximately ten days.
### Development Methodology and Testing

Throughout the project, we will employ unit testing and comprehensive testing to ensure the reliability and security of the E2EE solution. The agile Scrum approach, combined with Jira for project management, will enable our team to adapt to challenges, incorporate feedback, and iterate on the solution efficiently.

(https://hermanyiqunliang.atlassian.net/jira/software/projects/YIQ/boards/2?atlOrigin=eyJpIjoiZThkMmIyOWI5YzUxNDQ2NjhhNWI1ODAxZWMyMDljOGUiLCJwIjoiaiJ9) 
### Cost and expenses
### Continuity and Future plan






