- My Reading Speed: 140 Words/ min, expected length: 2240
# Introduction
Good morning, professors. I am really glad to have a chance to bring you my dissertation project, the WeChat End-to-End Encryption Tool, which I want to call it, the Libre Chat. 
# Motivation
The first reason is it has a big user number base. 
WeChat has over 1 billion daily active users. Tencent QQ has over 300 million daily active users. Ding Talk app, which has less than 100 million users, and it is more likely to be a Slack type organizational app. 
So, we can see WeChat has an undoubtful leading role here. 
## WeChat's privacy
However, there are some concerns. Does WeChat comply to the privacy needs? 
### Third Party Report
#### Amnesty International
The official Amnesty International's rank in 2016 indicates that WeChat received a 0, and ranked the bottom among all the researched applications. 
#### Citizen Lab Canada
The Citizen Lab of the University of Toronto has published many reports regarding the WeChat transparency and censorship. 
Just used one research paper as an example: It indicates WeChat has a real-time, automatic censorship of images using MD5 and hash. It also provides the other text filtering. The filtering is especially targeting politics news. 
There are also lots of technical reviews about how WeChat is filtering text and so on, but I would like to skip this part and introduce my personal experience. 
### News and Personal Experience
I am not an activist in politics, but these are the essential reasons why I made this project. 
#### Xiaobo Liu
Xiaobo Liu is a Chinese revolutioner, received a Nobel Peace Prize. He participated in many historical event including the protest on Tiananmen Square, and he died in 2017. The death of him results many discussions of democracy on Chinese social platforms. WeChat filtered all the English and Chinese spelling of his name to restrict the discussion. 
#### Peng Shuai 
Pengshuai has accused Gaoli Zhang, a Chinese vice prime minister, for sexual assault on Weibo. After three hours, the post was deleted by Weibo, and WeChat also start filtering the keywords and screenshots. I was attempting to send a screenshot. However, as I mentioned in the previous report, even if I edit the photos, those photos are still blocked. 
#### Sitong Bridge Protest

During the 2022 Chinese election, there is a protestor put a banner on the bridge in Beijing for anti-lockdown. I shared this to my friend on WeChat. Right after I share the image, I was banned for 7 days. 
On the same time, my grandpa, which is a 75 years old man, has been working for this country for his lifetime, was banned for spreading rumours. In fact, he was sent news regarding the prediction of the election in the WeChat group.  
#### Others
Some others cases I tested but failed. 
### Any Other Choices For Mainland People to use E2EE? 

### Using VPN
When I was in mainland, I was trying to use VPN to chat with my friends with WhatsApp and Telegram. I believe the connection is secure, but there are a few drawbacks. First, the connection is not stable. Second, I attempted to keep the VPN always on, but finally failed. Many Chinese native apps do not support foreign IP addresses. (company registry app/some bank loan app/video app/ driver licence management app, and so on) It is unable for people to switch the VPN off while they are watching the videos, and turn the VPN on after they finish watching. Even if they can do that, they will lose the messages when they are watching the videos. Third, personal use of VPN is illegal and has a potential fine of thousands of RMB. 
### Own a foreign SIM card
Many people bought UK SIM cards during the pandemic, so that they can connect to Warwick university services. It is stable, legal and safe to use. However, the card has the same drawbacks as the VPN. We cannot keep it always on, and it is super expensive. 
### Any similar solution before
Through the searching on GitHub, I observed that there is a thinking about WeChat E2EE implementation. However, WeChat does not support the Web version any more, it will redirect most users to use the Desktop version.  ![[Pasted image 20240414170049.png]]We believe that is because of some special commercial considerations of WeChat, but that eventually increases the complexity for us to provide users a end to end encryption experience. 
# Demonstration
Before I tell you the tech part, I would like to show my current work first to give you are general view. This is just the work so far. I plan to implement a lot of stuff including multi language support and so on. 

For this part, I would say sorry to Dr. Feng Hao, because I didn't have much progress after February on the Windows version. However, I did finish a simple example of my mobile version. 
## Electron
Injection
Get a New Key
Copy a Key
Send and Receive Messages
## Android
Get a New Key
Copy a Key
Send and Receive Messages
# Design, Tech and Tech Stack

Our main goal is to allow all the Chinese users to have a safe, encrypted conversation with the lowest effort. We want to make the tool 1. WeChat based, 2. End-to-End Encrypted Message, 3. Easy to use, 4, Legal, and cannot be blocked. Then I will show you how I am going to achieve this. 
## Windows
For making a such product, we cannot leave the usage of many kinds of utilities. Therefore, to inject the WeChat, I used wxhelper(https://github.com/ttttupup/wxhelper/tree/main) project and the Electron Spoiler Template to start. The wxhelper is an open source WeChat injector. It updates every 3 months to make sure they can catch up to the latest WeChat release. The Electron Spoiler is the best Electron template I can find on the internet. It follows every security requirement and configuration that Electron suggests. 
So, when a message comes, it will be intercepted by the wxhelper, delivered to our app, and our app read it, decrypt it, and display it to the user. When a user sends a message, it will encrypt it and send it through the wxhelper. 
## Android
The injection is possible, but hard for the users. Usually the injection requires the usage of root privilege, but many phone manufactures are limiting the usage of it.  
Usually, if a normal user wants to decrypt or encrypt a message, the users are required to copy it, and then open a third party website or app, paste it, and then get the result. That is NOT convenient. However, when we look into this process, we can see the time we took the most is copy and pasting. How about let's set up a function within the keyboard, so that the users don't have to jump from 1 app to another. 
Therefore, my idea is to make a keyboard that when you receive a message, copy it, then it will be automatically decrypted, and when you are sending a message, there is a button, tap it, and encrypt it. 
It sounds not reality to create a keyboard on our own. However, which keyboard should we use to begin? 
When I was trying to find a keyboard to make a plug in. What brings to my mind is that the keyboard must be open sourced, secured and fully offline. Fcitix /ˈfaɪtɪks/ (**Free Chinese Input Tool for X**) is the largest community maintained Chinese input method. It satisfied everything I required. So, we mainly edited their keyboard's clipboard part, and another part on their input view to implement the E2EE feature. 
After I finished the implemented, there is very recent research published on Apr.23 which verifies what I just talked. It reveals that most of the Chinese keyboards are leaking your personal information. This is already fixed. However, it proves that a keyboard is connected to the internet, it still has the potential possibility to leak your information. So, I believe for me it is correct to use Fcitix. 
## Protocol
The main protocol we are using now is the RSA protocol, because it is easy to use, well known, and reliable. 
We might have some updates regarding other protocols, such as Signal. 


# Issues
## Android ⇿ Windows
The encryption method for both Android and Windows are RSA-2048/OAEP Padding. The keys are PEM format. However, there are still some issues for connecting them together. 

## WeChat Update
We have noticed that WeChat could implement a force login restriction when the version is too low. There are two ways for us to solve this. From one hand, the open source GitHub, and probably I will continue to update WeChat Injection scripts. On the other hand, there are already some injection scripts to avoid the WeChat update by changing their version number. So, we aim to connect these scripts seamlessly to our app. 
## WeChat Potential Architecture Change
As we may already know, that Tencent recently updated the QQ architecture from C++ to Electron, which is actually the framework we are using now. The reason for them to change it is to save its multi-platform developer cost. If the architecture of WeChat changes, our app would become deprecated and cannot be regularly updated. 

## WeChat Implemented E2EE Function
If in the future, WeChat one day implemented the E2EE function, this project will be useless. This is a key threat to my project. However, I would say If this is announced, I will be really satisfied instead of being disappointed to see my 3-month effort becomes useless, because it is finally a great thing for the users. 

# Current Process and Schedule 

As you can see from this timeline, I have worked on the Electron Windows version back to February and finished my design at that time. I have finished my Mobile version on April. I will also work on it after the exam. Then I will improve it after that. 
Starting March, I started to work as a full-time employee in charge of Electron app development remotely at a Canadian company. Furthermore, I was also working as a part-time intern at another Canadian company. I have my final exams in May and June. Physically, I will back to Canada for working on-site after that. Our time is very tight. 
However, I would say there are also benefits. Since I worked on this E2EE app, I got the full-time job, and since the full-time job, I can learn more about Electron. I learned how to manage the child process, use code to inject another app, get the admin privilege I also learned which DB will be best fit our chat history storage. 
Back to our schedule, I believe the main time I will work on this will be in June, to make it almost done, and will improve it later after the interim report. 

# Use of GPT
Before these months, I have zero experience regarding Electron and Android Development. I know it is not possible for me to become an expert, or a senior developer in such a short time. Luckily, the generative tools act as an intermediate developer for me. It fixes my grammar mistake and give me suggestions on the best security practices. 

# Conclusion
I hope this project could bring the people in China a new integrated E2EE experience with WeChat when it is finished.  Questions and Comments. 