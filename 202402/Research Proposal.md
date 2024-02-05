## Motivation
Most convenient WeChat's monitor on user's data
E2EE's introduction
China does not allow a registered real E2EE app in China and related laws
China does have a firewall to prevent users use abroad E2EE apps (WhatsApp, Facebook Messenger, etc. ). Some users use VPN, but  VPN also have potential illegal status. VPN connection not stable, because large VPN providers are targeted by Chinese gov. Small VPN providers are generally not safe. 
## Ideas
Therefore, we need to make a offline tool to achieve E2EE functions within the app through WeChat platform. 
We should use WeChat hook to retrieve the message from WeChat application and forward it to a HTTP port. Also, this hook also needs to receive a post message to a HTTP port.  our application. our application, to retrieve the message. 