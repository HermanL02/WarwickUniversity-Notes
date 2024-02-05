## Motivation
Most convenient WeChat's monitor on user's data
E2EE's introduction
China does not allow a registered real E2EE app in China and related laws
China does have a firewall to prevent users use abroad E2EE apps (WhatsApp, Facebook Messenger, etc. ). Some users use VPN, but  VPN also have potential illegal status. VPN connection not stable, because large VPN providers are targeted by Chinese gov. Small VPN providers are generally not safe. 
## Ideas

### Function design
The encryption protocol we need to choose a type that can easily exchange them online, which here I think a RSA protocol would be a good beginning. After the app is fully implemented, we can add more protocols including J-Pake (developed by Dr. Feng Hao, references) and Signal. 

The basic function is that it can encrypt and also decrypt the message. Supposing there are two people, A and B, are trying to do the encrypted communication is using this app. User A should be able to retrieve a WeChat message that, decrypt it using A's private key and also should send a WeChat message that encrypt it using B's public key. 

The application should allow users to exchange public keys by direct user inputs and also to bind their WeChat unique ID and store the public key to the cloud for quick exchange. 

## Implementation 
We should use WeChat hook to retrieve the message from WeChat application and forward it to a HTTP port. Also, this hook also needs to receive a post message through the API. Fortunately, there is a open source GitHub repo to provide this function. 



