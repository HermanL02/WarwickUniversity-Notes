## Intro
In the midst of the digital revolution, network security is becoming a crucial factor for data integrity, confidentiality and availability. As the network attacks grow in both frequency and complexity, the importance to enforce security protocol to protect the data transmission has become increasingly apparent. In this context, TLS, as the base of protecting network transmission, played an pivotal role. 

TLS 1.2 is a widely used standard in the production standard, its design reflects the network security environment's requirement and challenge in the current stage. However, as the time passing by, the changing of the threaten models, and the growing of computing limit, TLS 1.2 has exposed many security flaw and the performance limitation. These challenges promotes the creation of TLS1.3. It not only strengthened security standard, but also improved efficiency and performance. One of the feature is that TLS 1.3 used simplified handshake process and stronger cryptographic primitives to provide enhanced security level and improved performance. 

Despite the theoretical and practical superiority of TLS 1.3, it is still a challenge for websites to deploy it in production. The challenges including the combability with current system, the cost and complexity to upgrade, and the understanding of new features. Since these reasons, TLS 1.2 is still widely used, although we know the security drawbacks.  

This essay will deeply explore and analyse the design, security, performance and the applications in the real world, and will do critical analysis to the leading documents. 

## Source Choosing

The thesis, "The Era of TLS 1.3: Measuring Deployment and Use with Active and Passive Methods", uses the method of active scanning and passive monitoring method to measure the use and deployment of TLS 1.3. The target is to measure TLS 1.3's application since IETF standard, and mainly discussed the influence of cloud providers and CDN  to TLS 1.3's fast deploy. 

During their investigation, they found that TLS does use the functions we mentioned above. However, the deploy of TLS 1.3 is too concentrated, which means all the connections are stopped at some specific providers. It means that the servers are not widely spread. 

It generally combines different data sources and methods to provide a broad view of TLS 1.3 environment. However, it also reveals that there are some limitations. Their research are regional limited. The passive sniffing only concentrated in North America and Australia. It does not consider other regions as well as other language speakers. Besides, the data collection are having some issues. It does not collect the data from the latest IPV6 network, and it does not consider the latest extension of TLS 1.3, such as the certificate authority and the client side verifications. It means it actually cannot fully evaluate the new features and new effects. 

In the essay of ### A Cryptographic Analysis of the TLS 1.3 Handshake Protocol