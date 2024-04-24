- My Reading Speed: 140 Words/ min, expected length: 2240
# Introduction
Good morning, professors. I am really glad to have a chance to bring you my dissertation project, the WeChat End-to-End Encryption Tool, which I want to call it, the Libre Chat. 
# Motivation
## WeChat Market Place
According to the latest data of Chinese instant message apps, WeChat ranked the top, which has over 1 billion daily active users. The second one is QQ, which has over 300 million daily active users. It is also a Tencent product. The third one would be Ding Talk app, which has less than 100 million, and it is more likely to be a Slack type organizational and administration app. We may observe that WeChat has a dominant role in China. 
## WeChat vs. Privacy
However, there are some concerns. Does WeChat comply to the privacy requirements? 
### Third Party Review
First, I will talk about the official Amnesty International's rank in 2016. This is the only official evaluation that I can reference here. In this metrics, WeChat received a 0 in evaluation and ranked the bottom. 
However, that is already out of date, so, second, I will talk about the technical methods. 
### Technical methods 
If we briefly take a look at the technical methods WeChat use to protect the security compare to its competitors. It is the only app that does not provide a E2EE option, while it only provides the encryption between the users and the server, which means this is still technically possible to be leaked to WeChat workers and the government. Telegram provides a E2EE option. WhatsApp, Facebook Messenger, and iMessage all provide real time end-to-end encryption protocol. 
### Personal Experience
Although there is no official investigations about how many users are not satisfied with the WeChat privacy policy, I could provide some personal cases about it. 
During the 2022 Chinese election, there is a protestor put a banner on the bridge in Beijing for anti-lockdown. I don't personally agree or disagree with the person, but I shared this to my friend on WeChat. Right after I share the image, I was banned for 7 days. 
On the same time, my grandpa, which is a 75 years old man, who sent news regarding the prediction of the election in the WeChat group. He was banned as well as the whole WeChat group for spreading rumours. 
Above 3分20秒
### Other Apps
### Using VPN
### Any products before? 
Through the searching on GitHub, I observed that there is a thinking about WeChat E2EE implementation. However, WeChat does not support the Web version any more, it will redirect most users to use the Desktop version.  ![[Pasted image 20240414170049.png]]

# Design

Our main goal is to allow WeChat users to have a safe, encrypted conversation with the lowest effort. We want to make the tool 1, Easy to use, 2, Legal, Cannot be blocked
How to easy to use? How to Legal? And How to be not blocked?
## Why not website? WeChat weird design. 
## Windows
## Android
Besides core: Sharing Contacts! 
# Tech and Tech Stack

## Frameworks
### Windows
We will use Electron as the framework, with React.js as the frontend, and Node.js as the backend. 
## Reverse Engineering
## Encryption
## Test and Decentralized


# Schedule 
Sorry for a little bit of show off here. I am balancing my work, study, and the project. 

# Work