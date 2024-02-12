## Motivation
Most convenient WeChat's monitor on user's data
E2EE's introduction
China does not allow a registered real E2EE app in China and related laws. 
China does have a firewall to prevent users use abroad E2EE apps (WhatsApp, Facebook Messenger, etc. ). Some users use VPN, but  VPN also have potential illegal status. VPN connection not stable, because large VPN providers are targeted by Chinese gov. Small VPN providers are generally not safe. 
## Ideas

### Platform Support
The app will mainly focus on Windows and Android phones, because my current develop environment is Windows and Android. I don't have MacOS and iPhone devices. If it is possible, we will introduce our app on more 

On Windows, we want to use WeChat hook to achieve direct chat using our app, through WeChat platform. (We will introduce details later.)  The app will be build with Electron Framework, with React.js as front end and Node.js as backend. The app will rely on IPC communication. 

On Android, due to the limitation of retrieving root privilege on Android devices, we decided to extend the current keyboard app to add another plugin using Kotlin. 

In the future, we will deploy a server using Node.js to create APIs for users to upload their public key with their WeChat unique ID and retrieve others public key using WeChat unique ID. However, we want to make sure when the server is blocked or is down, the app is still usable. 
### Function design
The encryption protocol we need to choose a type that can easily exchange them online, which here I think a RSA protocol would be a good beginning. After the app is fully implemented, we can add more protocols including J-Pake (developed by Dr. Feng Hao, references) and Signal for easier and safer key exchange. 

The application should allow users to exchange public keys by direct sending messages. The basic function is that it can encrypt and also decrypt the message. 

Supposing there are two people, A and B, are trying to do the encrypted communication using this app. User A should be able to retrieve a WeChat message and decrypt it using A's private key and also should send a WeChat message that encrypt it using B's public key. 


## UX design

## Implementation 
For Windows system, we should use a WeChat hook to use reverse engineering to retrieve the message from WeChat application and forward it to a  local HTTP port. Also, this hook also needs to receive a post message through the API. There is a open source GitHub repo to provide this function. (reference) 

For Android system, we will based on [fcitx5-android](https://github.com/fcitx5-android/fcitx5-android) , which is an app with thousands of stars. This keyboard mainly based on local dictionaries with regular updates. It does not send the user input to any other third parties. 

## Target customers

## deliverable and work plan
### Cost and expenses
### Continua

The development will based on scrum development and will use Jira to manage the development. The development will cost around 2 months. The first month will be focused on Windows application design. The second month will be focused on Android application design. 

The development will be step by step, which are learning framework, develop backend process, develop frontend logic, UI/UX implementation, unit tests and general test. Learning and implementations will cost 8 days each and the tests will cost 2 days each. The rest time will be assigned to unexpected errors. 

The Windows development is already started. The Jira process can be found here. https://hermanyiqunliang.atlassian.net/jira/software/projects/YIQ/boards/2?atlOrigin=eyJpIjoiZThkMmIyOWI5YzUxNDQ2NjhhNWI1ODAxZWMyMDljOGUiLCJwIjoiaiJ9



