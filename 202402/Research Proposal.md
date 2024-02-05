## Motivation
Most convenient WeChat's monitor on user's data
E2EE's introduction
China does not allow a registered real E2EE app in China and related laws
China does have a firewall to prevent users use abroad E2EE apps (WhatsApp, Facebook Messenger, etc. ). Some users use VPN, but  VPN also have potential illegal status. VPN connection not stable, because large VPN providers are targeted by Chinese gov. Small VPN providers are generally not safe. 
## Ideas
### Requirement and 底线 design
We want to make a E2EE app to achieve E2EE communication between the users. I set up 4 requirements of this app. First, it is a open source code itself.  it only uses open source code to ensure safety. Second, it complies the current Chinese/UK and most countries legal requirement. Third, it should be used easily and quickly by most users. Fourth, it should ensure the safety of its protocol. 

### Function design
To make sure it can should accept a user input to encrypt the user input, and it


The should allow users to generate a encrypted text message using public key.
We should use WeChat hook to retrieve the message from WeChat application and forward it to a HTTP port. Also, this hook also needs to receive a post message through the API. Fortunately, there is a open source GitHub repo to provide this function. 



