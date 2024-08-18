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
## Concepts Application
For the last several months, I have learned many essentail software development skills and applied them to our apps. The app design concepts  are usually a foundation of the whole software development process. 
### Coupling and Cohesion
The high coupling refers to a situation where modules are highly dependent on each other. It means changing one module might require changes in several other modules as well. The low cohesion means that the functions within a module are not closely related and the module might be responsible for too many unrelated tasks or a module contains too many unrelated functions. The combination of these two issues might lead to code that is difficult to maintain and hard to extend.    
This issue is extremely difficult in Electron, because both frontend and backend code are in JavaScript. It means some functions can be done on the frontend, and they can be done on the backend as well. If the modules are not designed properly, the coupling will be very high. 
To avoid this issue, we follow the module design principle. During the development in Electron development. In the software, we separate the frontend logic and the backend logic. The basic principle is everything related to data will be strictly limited to only be processed on the backend, and everything regarding the interface will be strictly limited to the frontend. Therefore, even if the frontend and the backend changes, they will not influence each other, to afford a low coupling and high cohesion application. 

## Comments Reducing
Regarding comments, it is really controversy. Many code examples encourage writing clear comments and docs. However, during the development process and the advice of my colleagues, I realized that the code readability is not really achieved by massive comments. It is based on clear and simple naming. When a software is designed in a good structure, the name of the function and the name of the variable could be meaningful and express their utilities. The comments will be 


- 总体思路: 过去的Electron开发经验
- 添加 高耦合低内聚
- 添加 软件开发理念 例如学到的减少注释 名字简洁则是最好的注释
# Process

## Solved Issues 
## Remain Unsolved Issues


# Issues
 - 添加 Express Server stall?
 - 添加 Hook成功但是无法收到消息, 需要重启，猜测可能的原因

# Project Management
- 添加 Debug (live debug)
- 添加 Issues during coding: → Clarity and maintenance; ESLint and Prettier ?(只有上帝和我知道代码)
- 添加 测试结果


# Potential Threats
- 添加 wxhelper版本的具体问题 比如部分版本提供的功能不同
- 添加 微信可能的反制措施


# Unachieved Features
- 添加 多语言的实现方法, 以及为何最终未能实现，即使是公司的软件也没能实现
- 多端同步 为什么没能实现 以及我们所作的努力和尝试 例如导入钥匙等
- Jest 未能实现 为什么? 为什么他很重要? 

# Acknowledgement

感谢 导师 女朋友 
感谢 Syed，作为Koii Network的Chief of Engineering 给的建议
Pablo, Senior Developer 

