## Motivation
## Background
Nowadays, the balance between convenient communication and privacy has become a serious concern. In an era that digital communication is everywhere, the convenience of keeping communication with others seems to be granted. However, this convenience brings a strict privacy issue, because most governments and enterprises are seeking or having the ability to monitor, collect and analyse much personal communication data. 

End-to-End Encryption (E2EE) is a safe communication method, which can prevent third party to retrieve the data when transmitting the data from one terminal or device to another terminal or device. It means all other external entities including the government, telecom providers, Internet providers, and even the service providers themselves do not have access to the messages. 

Many countries in the world take terrorist, crime and national security threats as the reason to restrict encryption attempts, including E2EE technologies. This situation shows that although E2EE provides privacy advantages, there is resistance with implementations. Some governments believe that E2EE technologies make the criminal's communications cannot be censored and monitored. Many countries are attempting to take legal act of tech companies that provide E2EE services. These actions result in a serious discussion between privacy and the possibility of misuse of the rights of monitoring. It shows that it is hard to balance security and personal information. 

China is always in the forefront of monitoring chat communications, implementing strict regulations and use advanced technologies to monitor and censor online activities. The Chinese government is trying to monitor public and personal digital communications and filter anything political sensitive or harmful to national benefits. In this situation, the use of E2EE causes a challenge of government's control and monitoring personal chats. Therefore, the real E2EE apps are facing a challenge to pass the Chinese government's review. This act is in line with larger internet governance policies in China, including the Great Firewall, which blocks access to many foreign websites and services, including popular applications like WhatsApp and Facebook Messenger. Also, in some cases, the police officer would stop you on the street to see if you are using some illegal apps, like Telegram. 

One notable example is WeChat, China's most popular messaging app, which offers many services, from messaging to financial transactions. However, its convenience comes at a cost. Its significant monitoring and data collection practices that raise privacy concerns. WeChat's approach to user data represents the trends in digital surveillance and data management within China. 

To circumvent these restrictions, some users turn to Virtual Private Networks (VPNs), which can provide a way to access blocked services by encrypting the user's Internet traffic and routing it through a server located outside of China. However, the use of VPNs in China is challenging for normal users. First, the legal status of VPNs is ambiguous and potentially illegal if not government-approved. It makes their use risky. Moreover, the Chinese government has been known to target large VPN providers, leading to unstable connections and further diminishing the reliability, such as NordVPN and ExpressVPN. Smaller VPN providers, on the other hand, may offer less security and are generally considered unsafe due to their lack of robust infrastructure and potential vulnerability to surveillance and data breaches.

## Ideas
The proposed solution involves developing mechanisms to enable easy established legal, stable E2EE for users within restrictive digital environments using non-E2EE popular app, WeChat, without connecting to outside Chinese servers and without using VPNs. 
### App Structure
### Windows
For the Windows operating system, we implemented two methods to address different scenarios. The first method is the basic condition, where the user utilizes our app to encrypt plaintext and decrypt ciphertext without the need for WeChat. This approach does not differ significantly from other online encryption tools, except for the management of secure friend's public keys and the user's private key. The second method is a highly convenient strategy. Our approach involves using a WeChat hook to apply reverse engineering techniques. This method is designed to intercept messages from the WeChat application, extract them for E2EE (End-to-End Encryption) processing, and then forward these encrypted messages to a local port. At the same time, this hook is configured to receive encrypted messages through a local API, decrypt them, and then display them within our application. Moreover, users can send messages through our app on WeChat. Users can input plaintext in our software, which is then forwarded to another port. The WeChat hook can then send the message to the contact via WeChat. The app will be developed using the Electron Framework, with React.js for the frontend and Node.js for the backend. The app will depend on IPC (Inter-Process Communication) for functionality.
### Android

On the Android platform, we have decided to enhance our current keyboard app by adding a new plugin using Kotlin. Our strategy utilizes the [fcitx5-android](https://github.com/fcitx5-android/fcitx5-android) application, which enjoys robust community support. This input method, known for its reliance on local dictionaries and frequent updates, ensures that user inputs are not shared with third-party entities. This framework lays a solid groundwork for incorporating E2EE (End-to-End Encryption) capabilities.

Drawing on this application, we plan to integrate a textbox within the Android keyboard input. This textbox will capture user input, and when the user presses the send button on the keyboard, it will transmit the encrypted message to the intended recipient. Additionally, the input method will monitor the clipboard to decrypt messages that have been copied.

### Optional Server
We plan to deploy a server utilizing Node.js to develop APIs that allow users to upload their public key along with their WeChat unique ID, and to retrieve others' public keys using the WeChat unique ID. However, to ensure the app remains functional even when the server is blocked or down, we will implement additional resilience measures.

To enhance the app's resilience and usability during server downtimes, we will incorporate a local caching system within the app. This system will store recently accessed public keys and their associated WeChat IDs locally on the user's device. By doing so, the app can continue to facilitate the encryption and decryption processes by using the cached keys, ensuring that users can still communicate securely without interruption.

Moreover, we will explore the possibility of establishing a peer-to-peer (P2P) fallback mechanism. In this scenario, if the central server becomes unreachable, the app will attempt to connect directly with peers (other app users) to exchange public keys. This P2P approach leverages the users' network, making the system more robust against server outages and censorship efforts.

To further enhance data integrity and security, we will implement cryptographic verification of the public keys retrieved from both the server and peer sources. This ensures that the keys have not been tampered with, maintaining the trustworthiness of the encryption process.

These measures, combined with the server's existing functionality, will ensure that the app remains a reliable tool for secure communication, even in the face of server disruptions or network issues.

### Scalability

The proposed solution involves multiple encryption methods and the utilization of a WeChat hook within WeChat, designed to provide robust security and flexibility in communications. Below we explore various aspects of scalability and resilience of the system.

### Technology Scalability

Our app is designed to be highly scalable in terms of encryption technology. It allows users to choose from multiple encryption strategies, providing the flexibility to select or customize encryption methods. This design ensures that the app can adapt to new security challenges and prevents encryption methods from becoming obsolete.

However, the scalability of the WeChat hook for Windows presents unique challenges. The hook needs to be updated to remain compatible with new versions of WeChat. Given that WeChat may enforce updates, there could be a delay in updating our hooks to match the latest version, which might temporarily limit users to basic encryption methods until the hook is updated.

### Enhanced Operation Scalability

To ensure the app remains user-friendly and stable, we emphasize simplicity in its operation. The solution is designed to integrate seamlessly with users’ existing communication habits, minimizing the need for complex configurations. Our goal is to maintain an intuitive user experience that encourages continued use of the app, even as we introduce advanced encryption functionalities.

### Legal Status Scalability

While there are potential legal challenges, especially concerning the use of E2EE in regions with strict regulatory environments like China, our approach aims to mitigate these risks. By focusing on local app deployment and minimizing server reliance for critical operations, the app's visibility to regulatory authorities is reduced, enhancing its resilience against legal and regulatory actions.

### Server and Network Load Scalability

To further ensure the app’s reliability, key exchange can be conducted through the server or, optionally, directly between clients to reduce server and network load. This hybrid approach enhances the system’s scalability and ensures that the client-side application can function independently for extended periods without server interaction, aiming for at least 24 hours of error-free operation.

### Expanding on Scalability and Resilience

To address the potential latency in updating WeChat hooks, we will explore the development of a modular hook system that allows for quicker adaptations to new WeChat versions. This system could include a community-driven platform where developers can contribute updates and fixes for new versions of WeChat, fostering a collaborative environment that speeds up the update process.

Additionally, we will implement advanced caching mechanisms for encryption keys and user settings, ensuring that these can be stored securely on the device for longer periods. This approach not only improves the app's performance but also its autonomy from network conditions and server availability.

In terms of legal and operational scalability, we will continuously monitor regulatory developments and adapt our strategies accordingly. This may involve enhancing the app's stealth features or deploying decentralized network technologies to further obscure communication and reduce the likelihood of detection and restriction.

By addressing these aspects of scalability and resilience, we aim to create a secure, user-friendly, and legally resilient communication platform that remains effective and accessible across various operating environments and regulatory landscapes.

### Deliverables Overview

The project's objectives focus on implementing a highly effective Windows WeChat hook and ensuring the robustness and efficiency of encryption protocols. Below is a detailed outline of the deliverables aligned with these goals:

### Windows WeChat Hook Implementation

1. **Successful Application of the WeChat Hook**: The hook is seamlessly integrated with the Windows version of WeChat, enabling real-time message interception without disrupting the native app experience.
    
2. **Interception Accuracy**: Achieve 100% success rate in intercepting messages, ensuring no messages bypass the hook, thus maintaining the integrity of the encryption and decryption process.
    
3. **Latency Reduction**: The message delivery system, post-interception and processing (encryption/decryption), operates with a latency of under 100 milliseconds, enhancing the user experience by ensuring timely communication.
    
4. **Memory Management**: The hook is optimized for efficient memory usage, eliminating any memory leaks to ensure stable and prolonged operation of the WeChat application without degradation in performance.
    

### Encryption Protocol Effectiveness

1. **Error-Free Encryption and Decryption**: The implemented encryption and decryption algorithms function without errors, accurately processing messages to maintain confidentiality and integrity.
    
2. **Performance Standards Compliance**: The encryption and decryption processes meet predefined performance standards, balancing security with efficiency to not impede the user experience.
    
3. **Security Validation**: Conduct thorough security checks to confirm the encryption protocols are free from vulnerabilities (漏洞). This includes regular audits, penetration testing, and adherence to current best practices in cryptographic security to prevent potential exploits.
    

### Quality Assurance and Testing

- **Comprehensive Testing**: Implement a rigorous testing framework that includes unit tests, integration tests, and end-to-end tests to ensure all components function correctly as a cohesive system.
    
- **Performance Benchmarking**: Regularly benchmark the system's performance, especially focusing on the speed and resource usage of the encryption/decryption processes and the WeChat hook's impact on the overall system.
    
- **Security Audits**: Perform continuous security assessments, leveraging both automated tools and manual inspection techniques to identify and mitigate any security issues promptly.
    

### Documentation and Support

- **Technical Documentation**: Provide detailed documentation covering the setup, configuration, and operation of the WeChat hook and encryption protocols, including troubleshooting guides and best practices for users.
    
- **User Support System**: Establish a responsive support system for users to report issues, request features, or seek help with the application, fostering a community-driven improvement process.
### Work Plan Overview

The development of the end-to-end encryption (E2EE) solution for WeChat on Windows and Android platforms will be approached using an agile methodology, specifically adopting the Scrum framework, tailored for a solo development effort. This approach ensures flexibility, rapid iteration, and continuous feedback throughout the project lifecycle. Project management and task tracking will be facilitated through Jira, allowing for clear visibility of progress and efficient organization of tasks. The overall development timeline is estimated at approximately two months, with distinct phases allocated to the Windows and Android platforms.

### Phase 1: Initial Setup and Planning (Weeks 1-2)

- **Sprint 0: Project Kickoff and Requirements Gathering**
    - Establish project goals, gather requirements, and define the scope for both the Windows and Android platforms.
    - Set up the project environment in Jira, creating epics and stories for initial tasks.
    - Outline the solo development strategy, incorporating roles such as Scrum Master and Product Owner into personal workflow.

### Phase 2: Windows Platform Development (Weeks 3-5)

- **Sprint 1: Windows WeChat Hook Development**
    
    - Design and implement the initial version of the Windows WeChat hook for message interception.
    - Begin development on the encryption module, focusing on integrating selected encryption algorithms.
    - Conduct initial testing and debugging of the hook and encryption module.
- **Sprint 2: Enhancement and Optimization**
    
    - Optimize the WeChat hook for performance, ensuring low latency and memory efficiency.
    - Enhance the encryption module, implementing security checks and performance optimizations.
    - Conduct thorough testing, including performance benchmarking and security audits.

### Phase 3: Android Platform Development (Weeks 6-7)

- **Sprint 3: Android App Development**
    
    - Start the development of the Android keyboard plugin, integrating the E2EE functionalities.
    - Implement the text box for input and configure clipboard monitoring for decryption.
    - Initiate testing for functionality, performance, and security on the Android platform.
- **Sprint 4: Finalization and Testing**
    
    - Finalize the development of the Android platform, focusing on refining features and fixing bugs identified during testing.
    - Perform comprehensive end-to-end testing across both platforms to ensure interoperability and reliability.
    - Address any remaining issues and conduct a final review.

### Phase 4: Deployment and Feedback (Week 8)

- **Sprint 5: Deployment and Market Introduction**
    
    - Prepare for deployment, including final documentation and user guides.
    - Deploy the E2EE solution for WeChat on both Windows and Android platforms.
    - Monitor the solution in real-time operation, collecting feedback for future improvements.
- **Post-Launch: Continuous Improvement**
    
    - Analyze feedback and performance data to identify areas for improvement.
    - Plan and implement updates in subsequent iterations, continuing to use the agile framework for ongoing development and enhancement.

Regular Scrum activities such as sprint planning, reviews, and retrospectives will be adapted for solo execution, ensuring the project remains on track, adapts to any changes or challenges, and continuously improves based on self-assessment and feedback.


### Continuity Plan

Ensuring the long-term viability and adaptability of the end-to-end encryption (E2EE) solution for WeChat on Windows and Android platforms requires a well-structured continuity plan. This plan will focus on maintaining operational effectiveness, addressing emerging threats, and incorporating technological advancements.

1. **Regular Updates and Maintenance**: Commit to a schedule of regular updates to the E2EE solution, including both the WeChat hook and encryption algorithms. This will address any security vulnerabilities that emerge and adapt to updates in the WeChat application itself.
    
2. **Community Engagement and Feedback**: Establish a mechanism for collecting feedback from users and engaging with the broader community. This feedback loop will be invaluable for identifying issues, understanding user needs, and prioritizing future developments.
    
3. **Scalability and Performance Optimization**: Continuously monitor and improve the scalability and performance of the solution. This includes optimizing code, reducing latency, and ensuring the system can handle a growing user base without degradation in performance.
    
4. **Research and Development (R&D)**: Dedicate efforts to R&D for exploring new encryption methods, enhancing security features, and integrating cutting-edge technologies (e.g., quantum-resistant encryption) to stay ahead of potential threats.






