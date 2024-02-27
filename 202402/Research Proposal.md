## Motivation
## Background
Nowadays, the balance between convenient communication and privacy has become a pivotal concern. In an era that digital communication is everywhere, the convenience of keeping communication with others seems to be granted. However, this convenience brings a strict privacy issue, because most governments and enterprises are seeking or having the ability to monitor, collect and analyse much personal communication data. The global discussion about the monitoring of chatting tools has never stopped. 

End-to-End Encryption (E2EE) is a safe communication method, which can prevent third party to retrieve the data when transmitting the data from one terminal or device to another terminal or device, which means all other external entities including the government, telecom providers, Internet providers, and even the service providers themselves do not have access to the messages. 

Many countries in the world take terrorist, crime and national security threats as the reason to restrict encryption attempts, including E2EE technologies. This situation shows that although E2EE provides privacy advantages, there is resistance with implementations. Some governments believe that E2EE technologies make the criminal's communications cannot be censored and monitored. Many countries are attempting to legislative compel of tech companies that provide E2EE services. These actions result a serious discussion between privacy and the possibility of misuse of the rights of monitoring, showing the hardness of balancing security and protect personal information. 

China is always in the forefront of monitoring chat communications, implementing strict regulations and use advanced technologies to monitor and censor online activities. The Chinese government is trying to monitor public and personal digital communications and filter anything political sensitive or harmful to national benefits. In this situation, the use of E2EE causes a challenge of government's control and monitoring personal chats. Therefore, the real E2EE apps are facing a great barrier to pass the Chinese government's review. This stance is in line with broader Internet governance strategies in China, including the Great Firewall, which blocks access to many foreign websites and services, including popular E2EE-enabled applications like WhatsApp and Facebook Messenger. Also, in some cases, the police officer would stop you on the street to see if you are using some illegal apps, like Telegram. One notable example is WeChat, China's most popular messaging app, which offers an array of services from messaging to financial transactions. However, its convenience comes at a cost: significant monitoring and data collection practices that raise privacy concerns. WeChat's approach to user data is emblematic of broader trends in digital surveillance and data management within China. To circumvent these restrictions, some users turn to Virtual Private Networks (VPNs), which can provide a way to access blocked services by encrypting the user's Internet traffic and routing it through a server located outside of China. Nevertheless, the use of VPNs in China is fraught with challenges. The legal status of VPNs is ambiguous and potentially illegal if not government-approved, making their use a risky endeavor. Moreover, the Chinese government has been known to target large VPN providers, leading to unstable connections and further diminishing the reliability of this workaround. Smaller VPN providers, on the other hand, may offer less security and are generally considered unsafe due to their lack of robust infrastructure and potential vulnerability to surveillance and data breaches.

## Ideas
The proposed solution involves developing mechanisms to enable easy established legal, stable E2EE for users within restrictive digital environments using non-E2EE popular app, WeChat, without connecting to outside Chinese servers and without using VPNs. 
### App Structure
### Windows
For the Windows operating system, we applied two methods to deal with different conditions. The first one is the basic condition, which is the user use our app to encrypt the plaintext and decrypt the ciphertext without using WeChat. This does not make any difference with other online encryption tools, except for the secure friends public key and the user's private key management. The second level is a veryr convenient method. Our strategy encompasses utilizing a WeChat hook to employ reverse engineering techniques. This method aims to intercept messages from the WeChat application, extracting them for E2EE processing, and then forwarding these encrypted messages to a local port. Concurrently, this hook is designed to receive encrypted messages through a local API, decrypt them, and then display them within our application. Also, the user can send message through our app on WeChat. The users can input plain text in our software, and then the message will be forwarded to another port. Then WeChat hook could send the message to the contact through WeChat. The app will be built with Electron Framework, with React.js as front end and Node.js as backend. The app will rely on IPC communication. 
### Android

On the Android platform, we decided to extend the current keyboard app to add another plugin using Kotlin. Our approach is based on leveraging the [fcitx5-android](https://github.com/fcitx5-android/fcitx5-android) application, which boasts significant community support. This input method, renowned for its reliance on local dictionaries and regular updates, guarantees that user inputs are not transmitted to third-party entities. This framework provides a secure foundation for integrating E2EE functionalities. 

Based on the application, we want to implement a textbox within the input Android keyboard, that could receive the user input, when user clicks on send on keyboard, it then will send the encrypted message to the designated user. The input method also monitors  the clipboard, to decrypt the copied messages. 

### Optional Server
We will deploy a server using Node.js to create APIs for users to upload their public key with their WeChat unique ID and retrieve others public key using WeChat unique ID. However, we want to make sure when the server is blocked or is down, the app is still usable. 

### Scalability

The solution is related to multiple encryption methods and the WeChat hook in WeChat. 
### Technology Scalability

The app will be scalable for choosing multiple different strategies in encryption, and could allow users to decide their own encryption methods to avoid the encryption methods become outdated. 

However, for Windows WeChat hook, the hook can be updated after the latest WeChat version is available. However, different hooks are fitting different versions of WeChat. If the WeChat forces the users to update the latest version, it would cause the latency to update the WeChat hooks. During this time, we can only provide the basic encryption methods to the users to run the app. 


### Operation Scalability
We should maintain the app to be easy and stable at all the time. If the solution requires the users to do complex settings and changes their communication experience, it may be a challenge to let them continue to work on that. 

### Legal Status Scalability
There are potential risks of Chinese government to restrict the use the local use of E2EE. However, local apps are relatively harder to be revealed by the government. 
### Server and Network Load
The exchange of keys through the server is optional. The local client side should be reliable for running at least 24 hours without any errors. 
## Target customers

## Target
We want to make our project scalable. 

## Deliverable and work plan
### Deliverables 
The Windows WeChat hook is successfully applied. The hook achives 100% interception. The message deliver latency is reduced to under 100ms. The hook does not have any memory leaks. 

The protocols of encryption are successfully used. The encryption and decryption does not have any error. The encryption and decryption meets the performance standard. The security checks to ensure the encryption level and with no 漏洞。
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






