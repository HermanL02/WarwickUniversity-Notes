## Motivation
## Background
There is a pressing issue regarding the balance between privacy and easy communication. At present, digital means of communication seems to be granted, and keeping in touch with others seems effortless. But this convenience is marked by a severe privacy problem as many governments and corporations seek or have powers to monitor, gather, and analyze most private personal communication data. 

As a secure communication method, End-to-End Encryption (E2EE) makes it impossible for third parties to acquire data while transferring it between devices. In this case, no one else apart from the sender and recipient has access to these messages, including the government, telecom companies, or ISPs, even the service providers themselves.

Many countries in the world take terrorist, crime and national security threats as the reason to restrict encryption attempts, including E2EE technologies. This situation shows that although E2EE provides privacy advantages, there is resistance with implementations. Some governments believe that E2EE technologies make the criminal's communications cannot be censored and monitored. Many countries are attempting to take legal act of tech companies that provide E2EE services. These actions result in a serious discussion between privacy and the possibility of misuse of the rights of monitoring. It shows that it is hard to balance security and personal information. 

China is always in the forefront of monitoring chat communications, implementing strict regulations and use advanced technologies to monitor and censor online activities. The Chinese government is trying to monitor both public and personal digital communications and filter anything political sensitive or harmful to national benefits. In this situation, the use of E2EE causes a challenge of government's control and monitoring personal chats. Therefore, the real E2EE apps are facing a challenge to pass the Chinese government's review.  This act is in line with larger internet governance policies in China, including the Great Firewall, which blocks access to many foreign websites and services, including popular applications like WhatsApp and Facebook Messenger. Also, in some cases, the police officer would stop you on the street to see if you are using some illegal apps, like Telegram. 

One notable example is WeChat, China's most popular messaging app, which offers many services, from messaging to financial transactions. However, its convenience comes at a cost. Its significant monitoring and data collection practices that raise privacy concerns. WeChat's approach to user data represents the trends in digital surveillance and data management within China. 

To deal with these restrictions, some users turn to use Virtual Private Networks (VPNs), which can provide a way to access blocked services and encrypt the user's Internet traffic. It can route it through a server located outside of China. However, the use of VPNs in China is challenging for normal users. First, the legal status of VPNs is ambiguous and potentially illegal if not government-approved. It makes their use risky. Moreover, the Chinese government has been known to target large VPN providers, leading to unstable connections and further diminishing the reliability, such as Nord VPN and Express VPN. There are not smaller, and not registered VPN providers, on the other hand, may offer less security and are generally considered unsafe due to their lack of robust infrastructure and potential vulnerability to surveillance and data breaches. One other thing is, users do not always keep connected to VPN. When they are gaming or if VPN is lagging, they are likely to disconnect from it, so the messages cannot be delivered real time. 

## Ideas
We proposed a solution to use the non-E2EE popular app WeChat in restricted digital environments, providing users with easy access to a legitimate stable E2EE without having to connect to a server outside of China or use a VPN. 
### App Structure
### Windows
For Windows operating systems, we implement two approaches to deal with different situations. 

The first method is for the basic condition. The user uses our app to encrypt plaintext and decrypt ciphertext, no need for WeChat. Apart from managing the public keys of secure contacts and the private keys of users, this approach is no different from other online encryption tools. 

The second approach is a very convenient strategy. Our approach involves using WeChat hooks to apply reverse engineering techniques. The method is designed to intercept messages from the WeChat app, extract the messages for E2EE processing, and then forward these encrypted messages to a local port. At the same time, this hook is configured to receive encrypted messages through the local API, decrypt them, and then display them in our application. In addition, users can send encrypted messages through WeChat app. Users can enter plaintext into our software and then the software will forward it to another port. The WeChat Hook can then send the message to the contact via WeChat. The application will be developed using the Electron Framework, with React.js as the front end and Node.js as the back end. The application will rely on the functionality of IPC(Inter-process Communication) for isolate and secure connection. 
### Android

On the Android platform, we decided to enhance an open source keyboard application by adding a new plugin that uses Kotlin. Our strategy takes advantage of the [fcitx5 - android] (https://github.com/fcitx5-android/fcitx5-android) application, it has a wide range of community support. Although there is still little amount of people can access GitHub, it is still more accessible than other apps. This input method relies on local dictionaries and frequent updates, ensuring that user input is not shared with third-party entities. This framework provides a solid foundation for integrating E2EE(end-to-end encryption) capabilities.

With this application, we plan to add a text box into Android keyboard input. This text box will capture user input, and when the user presses the Send button on the keyboard, it will send the encrypted message to the intended recipient. In addition, the input method monitors the clipboard to decrypt copied messages. We will also design a contact management function.
### Optional Server
We plan to deploy a server that uses Node.js to develop APIs that allow users to upload their own public keys with WeChat unique IDs and retrieve the public keys of others using WeChat unique IDs. However, this is just a supplementary to our local software, which means even when the server is blocked or shut down, we still have access to the app. 

The app stores the recently accessed public key and its associated WeChat ID locally on the user's device. By doing so, the application can continue to use the cached keys to facilitate the encryption and decryption process, ensuring that users can still communicate securely without interruption.

In addition, we will explore the possibility of establishing peer-to-peer back-up mechanisms. In this case, if the central server becomes unreachable, the application will attempt to connect directly with the peer to exchange public keys. This P2P approach leverages the user's network, making the system more robust and resistant to server outages and censorship efforts. 

### Scalability

Below we explore various aspects of scalability and resilience of the system.

### Technology Scalability

It allows users to choose from a variety of encryption policies. We also try to provide the flexibility to choose or customize the encryption method. This design ensures that applications can adapt to new security challenges and prevents encryption methods from becoming outdated. 

However, the scalability of WeChat hooks on Windows presents unique challenges. The hook needs to be updated to remain compatible with the new version of WeChat. Given that WeChat may force updates, there may be delays in updating our hooks to match the latest version, which may temporarily limit users' access to only the basic encryption methods until the hooks are updated. 
### Enhanced Operation Scalability

To ensure the app remains user-friendly and stable, we emphasize simplicity in its use. We try to minimize the need for complex configurations. Usually the hook requires injecting WeChat first, then connect to WeChat, then send the message. We are working on writing it to the scripts to simplify the procedure. The solution is designed to integrate with users’ existing communication habits.  Our goal is to maintain an intuitive user experience that encourages continued use of the app, even as we introduce advanced encryption functions. 

### Legal Status Scalability

While there are potential legal challenges, especially concerning the use of E2EE in regions with strict regulatory environments like China, our approach aims to mitigate these risks. By focusing on local app and minimizing server reliance for critical operations, the app's visibility to regulatory authorities is reduced, enhancing its resilience against legal and regulatory actions.


### Expanding on Scalability and Resilience

To address the potential latency in updating WeChat hooks, I will be the first developer in charge of making updates, after that we could receive donations and use it as a reward to attract new developers to contribute updates and fixes for new versions of WeChat, fostering a collaborative environment that speeds up the hook's update process.

### Deliverables Overview

The project's objectives focus on implementing a highly effective Windows WeChat hook and ensuring the robustness and efficiency of encryption protocols. 

Below is a detailed outline of the deliverables aligned with these goals:

### Windows WeChat Hook Implementation
First, we need to make sure we have successful application of WeChat hook. The hook is along with the Windows version of WeChat. The real-time message interception without disrupting the native app experience should work well. 

Second, we need achieve 100% success rate in intercepting messages. It ensures no messages bypass the hook, thus maintaining the integrity of the encryption and decryption process.

Third, we need to minimize the latency by simplifying code. The message delivery system, post-interception and processing (encryption/decryption), operates without long latency. 
    
Fourth, as a known problem, the previous version of the WeChat hook has occasional memory leak problem. We need to be optimized for efficient memory usage. There is no memory leaks to ensure stable and long time operation of the WeChat application without degradation in performance. 
    

### Encryption Protocol Effectiveness

For Encryption protocol, first, we need to implement encryption and decryption algorithms function without errors. It should accurately process messages to maintain confidentiality and integrity.

Also, we need to conduct thorough security checks to confirm the encryption protocols are free from vulnerabilities. This includes regular audits, penetration testing, and adherence to current best practices in cryptographic security to prevent potential exploits.

### Quality Assurance and Testing

During the development process, we need to implement comprehensive testing that includes unit tests, integration tests, and end-to-end tests to ensure all components function correctly as a cohesive system. 

We need to regularly benchmark the system's performance, especially focusing on the speed and resource usage of the encryption/decryption processes and the WeChat hook's impact on the overall system.

We need to perform continuous security assessments, leveraging both automated tools and manual inspection techniques to identify and mitigate any security issues promptly.

### Documentation and Support

We need to provide detailed documentation covering the setup, configuration, and operation of the WeChat hook and encryption protocols, including troubleshooting guides and best practices for users.
    
We will use GitHub tickets to create a responsive support system for users to report issues, request features, or seek help with the application, fostering a community-driven improvement process.
### Work Plan Overview

The development of the E2EE solution for WeChat on Windows and Android platforms will be approached using an agile methodology, specifically adopting the Scrum framework, but a solo development. This approach ensures flexibility, rapid iteration, and continuous feedback throughout the project lifecycle. We will use Jira for real time feedback and visualization of our progress. It allows clear visibility of progress. The overall development timeline is estimated at approximately two months, with different phases allocated to the Windows and Android platforms. 


The first phase is the initial setup. I will spend two weeks to establish project goals, gather requirements, and define the scope for both the Windows and Android platforms. During this time, we will set up the project environment in Jira, creating epics and stories for initial tasks. 

The second phase is the Windows development. 

We will spend two more weeks on phase 2. We will design and implement the initial version of the Windows WeChat hook for message interception, and begin development on the encryption module, focusing on integrating selected encryption algorithms. 

We will conduct initial testing and debugging of the hook and encryption module, optimize the WeChat hook for performance, ensuring low latency and memory efficiency, enhance the encryption module, implementing security checks and performance optimizations.

We will conduct thorough testing, including performance benchmarking and security audits.

The third phase is the Android development for two weeks. 

We will start the development of the Android keyboard plugin, integrating the E2EE functionalities, implement the text box for input and configure clipboard monitoring for decryption.
We will initiate testing for functionality, performance, and security on the Android platform.
Also, we will finalize the development of the Android platform, focusing on refining features and fixing bugs identified during testing. We will perform comprehensive end-to-end testing across both platforms to ensure interoperability and reliability. Then I will contact some students to do the comprehensive alpha test. 

The fourth phase is the feedback phase for another one week. 

We will prepare for deployment, including final documentation and user guides, deploy the E2EE solution for WeChat on both Windows and Android platforms, and collecting feedback for future improvements.
    
I will do regular Scrum activities such as sprint planning, reviews, and retrospectives, ensuring the project remains on track, adapts to any changes or challenges, and continuously improves based on self-assessment and feedback.


### Continuity Plan

After finish the dissertation, we plan to ensure the long-term viability and adaptability of the E2EE solution for WeChat on Windows and Android platforms. It requires a well-structured continuity plan. This plan will focus on maintaining operational effectiveness, addressing emerging threats, and incorporating technological advancements.

We also may develop a new iOS and macOS version for better adaptability and making more users enjoy the secure communication. 

Commit to a schedule of regular updates to the E2EE solution, including both the WeChat hook and encryption algorithms. This will address any security vulnerabilities that emerge and adapt to updates in the WeChat application itself. This process will mainly rely on the rewards' system to attract more developers working on the updates to follow WeChat updates. 

We will also keep researching the new technologies such as quantum resistance techniques to remain our app up to date for new potential threats. 






