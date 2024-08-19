# Introduction
In today's digital era, instant messaging platforms have become integral to daily communication. To ensure the communication security, many users prefer to explore any secure communication software as their chat preferences. The popular choices are WhatsApp, Facebook Messenger and iMessage, which provides end-to-end encryption features supported by a variety of protocols. 

Meanwhile, in People's Republic of China(PRC), people cannot find a secure way to communicate. The secure apps we mentioned are not accessible due to the government applied internet restrictions. Instead, in the Chinese market, among all the communication applications and platforms, WeChat stands out with over 1 billion daily active users, making it a dominant force in the messaging area.  However, compare to their competitors on the global market, we found none of the Chinese apps provides an End-to-End Encryption(E2EE) feature, and none of them seen security and communication safety as their priority. This reveals a serious fact, which is over a billion users daily conversation is not protected and fully exposed to the company or the government. 

Therefore, we are here to introduce an E2EE solution for WeChat with main focus on Windows and Android platforms. The whole design has a tested workflow. Although it might not be a production level product to last decades, it potentially benefits people who can only access to the mainland chat applications and the people who need to keep contact with mainland friends. The whole idea also incentivize many more similar applications and urge WeChat and the government policies to change. 

For this application, we give it a name, Libre Chat. 
# Background and Research
# 功能展示 图片 
- 添加 安装微信
- 添加 反制微信更新

# Develop Structure 

## Windows
### Underlying Technology
- 添加 Process to use ICA to find vulnerabilities; SQL integration
- 
### General Structure
- NeDB
- 添加 Electron Builder How to include assets into installer
- 添加 Package Management NPM vs. YARN
- 添加 双向IPC通信 与 普通REST CALL的不同 为什么采用?
- 添加 inject Tool的选择分析
- 添加 ReactContext
- Key Formatting -> JSON.stringlify() 为什么普通格式不行? 为什么一定要JSON
### Back End
- 添加Java/C以及其他的bat反制微信更新作为backend
### Front End

## Android
### Structure

## Design Concepts

# Process

## Solved Issues 
## Remain Unsolved Issues


# Issues
## Express Server Stall
During the setting up of express server, there is some probability that the express server cannot receive the messages, but all other functions remain in the hook do not have any issue. 


# Project Management
## Concepts Application
For the last several months, I have learned many essentail software development skills and applied them to our apps. The app design concepts  are usually a foundation of the whole software development process. 
### Coupling and Cohesion
The high coupling refers to a situation where modules are highly dependent on each other. It means changing one module might require changes in several other modules as well. The low cohesion means that the functions within a module are not closely related and the module might be responsible for too many unrelated tasks or a module contains too many unrelated functions. The combination of these two issues might lead to code that is difficult to maintain and hard to extend.    
This issue is extremely difficult in Electron, because both frontend and backend code are in JavaScript. It means some functions can be done on the frontend, and they can be done on the backend as well. If the modules are not designed properly, the coupling will be very high. 
To avoid this issue, we follow the module design principle. During the development in Electron development. In the software, we separate the frontend logic and the backend logic. The basic principle is everything related to data will be strictly limited to only be processed on the backend, and everything regarding the interface will be strictly limited to the frontend. Therefore, even if the frontend and the backend changes, they will not influence each other, to afford a low coupling and high cohesion application. 

### Comments Reducing
Regarding comments, it is really controversy. Many code examples encourage writing clear comments and docs. However, during the development process and the advice of my colleagues, I realized that the code readability is not really achieved by massive comments. It is based on clear and simple naming. When a software is designed in a good structure, the name of the function and the name of the variable could be meaningful and express their utilities. The comments will be redundant and unnecessary. For example, 
```
// The following variable indicates whether WeChat is hooked
let k = false;
```
the above block is not as clear as the below one. 
```
let isHooked = false;
```
Therefore, by applying this rule, we reduced many keys 
### Over Engineering
Over engineering or early optimization is the mistake I made in this project. At the beginning of the project, we aim too much on designing the folder structure without the real requirement support. The general security standard is too high to ignore the real functionality design. Both resulted the development efficiency is low. 

At the beginning of the process, I was attempting to 
- 添加 Debug (live debug)
## Tools Utilization
## Live Debug
Developing an Electron app is similar to developing the web apps. Usually the web apps could apply the changes of the feature instantly and directly reflect instantly on the webpage. Electron framework inherits the benefits of web development while supporting the desktop app functions with multi-platform support. 
### Code Formatting
To maintain the clarity and maintenance of the code, it's essential to address common issues during coding. Therefore, in our project, I used ESLint and Prettier. ESLint helps in identifying and fixing code quality issues, while Prettier ensures consistent code formatting. By incorporating these tools into our development process, we not only make our code more readable to others but also to ourselves. As the saying goes, "Only God and I know what this code does... and sometimes even I'm not sure!" Proper formatting and linting help ensure that our code remains understandable, even as it evolves over time.

## 
- 添加 测试结果


# Potential Threats
## WXhelper Update
The project WXhelper is maintained by community members. Although the community members are keep contributing the new versions to follow up the WeChat versions, there are some minor changes are every update to make it not fully production reliable and hard to keep consistent update. For example, the API usually update very frequently and does not have a fixed pattern. For example, the type of the API calls route changes from the numeric numbers like `/api?type = 1` to meaning based routes like `/api/hookMessages`. 
It means every time they update their API, we might need to manually update it. That requires a continues distribution which this process can be interrupted by the third party.  

## WeChat Anti-Measures
It is possible for WeChat to block E2EE communications on WeChat. It depends on whether this worth them to do that. 
### Entropy
For example, the message contains encrypted messages usually have a high entropy and looks like random bit stream. WeChat could monitor the messages and identify the high entropy messages and mark them as a strong encrypted messages and may block these high entropy messages as well if they want. 
### Length
Also, since the RSA data length is fixed after the encryption and does not follow the plaintext's length to change. WeChat could also identify if the users have sent the messages of the same length. 
### 

# Unachieved Features
- 添加 多语言的实现方法, 以及为何最终未能实现，即使是公司的软件也没能实现
- 多端同步 为什么没能实现 以及我们所作的努力和尝试 例如导入钥匙等
- Jest 未能实现 为什么? 为什么他很重要? 

# Acknowledgement

感谢 导师 女朋友 
感谢 Syed，作为Koii Network的Chief of Engineering 给的建议
Pablo, Senior Developer 

