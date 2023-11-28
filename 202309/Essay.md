## Intro
In the midst of the digital revolution, network security is becoming a crucial factor for data integrity, confidentiality and availability. As the network attacks grow in both frequency and complexity, the importance to enforce security protocol to protect the data transmission has become increasingly apparent. In this context, TLS, as the base of protecting network transmission, played an pivotal role. 

TLS 1.2 is a widely used standard in the production standard, its design reflects the network security environment's requirement and challenge in the current stage. However, as the time passing by, the changing of the threaten models, and the growing of computing limit, TLS 1.2 has exposed many security flaw and the performance limitation. These challenges promotes the creation of TLS1.3. It not only strengthened security standard, but also improved efficiency and performance. One of the feature is that TLS 1.3 used simplified handshake process and stronger cryptographic primitives to provide enhanced security level and improved performance. 

Despite the theoretical and practical superiority of TLS 1.3, it is still a challenge for websites to deploy it in production. The challenges including the combability with current system, the cost and complexity to upgrade, and the understanding of new features. Since these reasons, TLS 1.2 is still widely used, although we know the security drawbacks.  

This essay will deeply explore and analyse the design, security, performance and the applications in the real world, and will do critical analysis to the leading documents. 

### Source Choosing

I would like to choose several sources. 

During the analyze, I will especially concentrate on 


## Analysis

In the Introduction to the Special Issue on TLS 1.3, part of the Journal of Cryptology, it outlines the development process of TLS 1.3, analyzes its security levels, and examines the challenges and opportunities in deploying it in real-world production environments. This introduction provides an overview of TLS 1.3, highlighting its collaboration with academia and the use of formal models to ensure a high security standard before publication.

The paper, "The Era of TLS 1.3: Measuring Deployment and Use with Active and Passive Methods," employs active scanning and passive monitoring techniques to assess the deployment and usage of TLS 1.3 since its standardization by the IETF. It primarily focuses on the impact of cloud providers and CDNs on the rapid deployment of TLS 1.3.

Their research confirms that TLS indeed utilizes the functions previously mentioned. However, the deployment of TLS 1.3 appears overly concentrated, indicating that most connections are channelled through certain specific providers, suggesting a lack of widespread server distribution.

This study integrates various data sources and methodologies to offer a comprehensive view of the TLS 1.3 landscape. Nonetheless, it also uncovers certain limitations. The research is regionally confined, with passive monitoring focusing on North America and Australia, neglecting other regions and non-English speakers. Additionally, there are gaps in data collection, such as the exclusion of data from the latest IPV6 networks and a lack of consideration for recent TLS 1.3 extensions like certificate authority and client-side verifications. This means it might not fully assess the protocol's newest features and impacts.

In the paper titled "A Cryptographic Analysis of the TLS 1.3 Handshake Protocol," the focus is on examining the handshake process through cryptographic analysis, especially concerning Full 1-RTT, PSK, 0-RTT, and PSK-(EC)DHE, including its optional 0-RTT variant. It demonstrates that the design of TLS 1.3 adheres to solid cryptographic principles, particularly highlighting the distinctiveness and separation of keys. The study also examines signatures and hashing in the security key allocation process and offers a precise account of the 0-RTT replay attack issue.

However, this research has its limitations. It lacks comprehensive coverage of the TLS 1.3 protocol, such as various cryptographic algorithms, signature schemes, Diffie-Hellman groups, and authenticated encryption schemes. It fails to ascertain security during the negotiation phase and does not account for the reuse of different algorithm combinations.

In the article on the Privacy of the TLS 1.3 Protocol, the focus is on investigating the privacy aspects of TLS 1.3. It primarily discusses the protocol's privacy protection throughout the handshake and conversation recovery processes. The article highly commends the design of TLS 1.3, highlighting improvements such as updated algorithms and earlier message encryption to enhance security and privacy. The investigation employs a privacy model to analyze privacy protection under various scenarios, including policies for AEAD and HKDF, with a special focus on the conversation recovery scheme.

The strength of this publication lies in its robust argumentation. It utilizes a game-based theoretical method, a widely recognized approach in cryptography research, to define and demonstrate the privacy protection of TLS 1.3. This methodology ensures that the investigation is both systematic and thorough. The article leverages mathematical and logical evidence, providing a strong theoretical foundation for evaluating TLS 1.3's features. Furthermore, it transparently acknowledges its limitations, specifically its narrow focus on selected scenarios, lending a balanced perspective to its conclusions.

However, there are areas that require further improvement. The article predominantly concentrates on theoretical analysis and overlooks practical considerations regarding the deployment and widespread usage of TLS 1.3.


