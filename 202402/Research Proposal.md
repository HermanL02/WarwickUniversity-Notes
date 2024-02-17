## Motivation
Nowadays, the balance between convenient communication and privacy has become a pivotal concern. One notable example is WeChat, China's most popular messaging app, which offers an array of services from messaging to financial transactions. However, its convenience comes at a cost: significant monitoring and data collection practices that raise privacy concerns. WeChat's approach to user data is emblematic of broader trends in digital surveillance and data management within China. 

The introduction of end-to-end encryption (E2EE) represents a technological solution to enhance privacy by ensuring that only the communicating users can read the messages. E2EE prevents potential eavesdroppers – including telecom providers, Internet providers, and even the service providers themselves – from accessing the cryptographic keys needed to decrypt the conversation.

However, the regulatory environment in China presents a unique challenge to the adoption of E2EE technologies. The Chinese government has not permitted the registration of real E2EE applications, citing national security and public safety concerns. This stance is in line with broader Internet governance strategies in China, including the Great Firewall, which blocks access to many foreign websites and services, including popular E2EE-enabled applications like WhatsApp and Facebook Messenger.

To circumvent these restrictions, some users turn to Virtual Private Networks (VPNs), which can provide a way to access blocked services by encrypting the user's Internet traffic and routing it through a server located outside of China. Nevertheless, the use of VPNs in China is fraught with challenges. The legal status of VPNs is ambiguous and potentially illegal if not government-approved, making their use a risky endeavor. Moreover, the Chinese government has been known to target large VPN providers, leading to unstable connections and further diminishing the reliability of this workaround. Smaller VPN providers, on the other hand, may offer less security and are generally considered unsafe due to their lack of robust infrastructure and potential vulnerability to surveillance and data breaches.

Therefore, it becomes imperative to explore a solution that enables the creation of genuine end-to-end encryption (E2EE) for communications within the Chinese region.
## Ideas
The proposed solution involves developing mechanisms to enable E2EE for users within restrictive digital environments without connecting to non-Chinese servers and without using VPNs. Based on this, we try to make the software as simple as possible. 
### Methodology
For the Windows operating system, our strategy encompasses utilizing a WeChat hook to employ reverse engineering techniques. This method aims to intercept messages from the WeChat application, extracting them for E2EE processing, and then forwarding these encrypted messages to a local port. Concurrently, this hook is designed to receive encrypted messages through a local API, decrypt them, and then display them within our application. Also, the user could input plain text in our software, and then the message will be forwarded to another port. Then WeChat hook could send the message to the contact through WeChat. 

On the Android platform, our approach is based on leveraging the [fcitx5-android](https://github.com/fcitx5-android/fcitx5-android) application, which boasts significant community support. This input method, renowned for its reliance on local dictionaries and regular updates, guarantees that user inputs are not transmitted to third-party entities. This framework provides a secure foundation for integrating E2EE functionalities. 

Based on the application, we want to implement a textbox within the input Android keyboard, that could receive the user input, when user click on send on keyboard, it then will send the encrypted message to the designated user. The input method also monitors  the clipboard, to decrypt the copied messages. 
### Function design
The cornerstone of our E2EE implementation is the selection of an encryption protocol conducive to online key exchanges. Initially, we propose the adoption of the RSA encryption protocol, renowned for its security and ease of key management. Subsequent iterations of the application will explore the integration of additional protocols, such as J-Pake and Signal, to enhance key exchange mechanisms and overall encryption security. 

The application should allow users to exchange public keys by direct sending messages. The basic function is that it can encrypt and also decrypt the message. 

Supposing there are two people, A and B, are trying to do the encrypted communication using this app. User A should be able to retrieve a WeChat message and decrypt it using A's private key and also should send a WeChat message that encrypt it using B's public key. 


## Target customers

## Deliverable and work plan
### Deliverables 
The app will mainly focus on Windows and Android phones, because my current develop environment is Windows and Android. I don't have MacOS and iPhone devices. If it is possible, we will introduce our app on more 

On Windows, we want to use WeChat hook to achieve direct chat using our app, through WeChat platform. (We will introduce details later.)  The app will be build with Electron Framework, with React.js as front end and Node.js as backend. The app will rely on IPC communication. 

On Android, due to the limitation of retrieving root privilege on Android devices, we decided to extend the current keyboard app to add another plugin using Kotlin. 

We will deploy a server using Node.js to create APIs for users to upload their public key with their WeChat unique ID and retrieve others public key using WeChat unique ID. However, we want to make sure when the server is blocked or is down, the app is still usable. 
### Work plan
The Windows development is already started. The work is disigned in 4 phases. The first phase is to get used to the development languagesThe Jira process can be found here. (https://hermanyiqunliang.atlassian.net/jira/software/projects/YIQ/boards/2?atlOrigin=eyJpIjoiZThkMmIyOWI5YzUxNDQ2NjhhNWI1ODAxZWMyMDljOGUiLCJwIjoiaiJ9) 
The main hard work will be focused on 
### Cost and expenses
### Continuity and Future plan

The development will based on scrum development and will use Jira to manage the development. The development will cost around 2 months. The first month will be focused on Windows application design. The second month will be focused on Android application design. 

The development will be step by step, which are learning framework, develop backend process, develop frontend logic, UI/UX implementation, unit tests and general test. Learning and implementations will cost 8 days each and the tests will cost 2 days each. The rest time will be assigned to unexpected errors. 




