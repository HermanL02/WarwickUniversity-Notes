# Question 1
## 1.1 Results and Screenshots
### SYN Flooding using C
Victim Machine: 
![[Pasted image 20231203020856.png]]
Virtual Machine: 
![[Pasted image 20231203020824.png]]
Virtual Machine: 
![[Pasted image 20231203020736.png]]
### SYN Flooding using Python 
Attacker: 
![[Pasted image 20231201014120.png]]
Victim: 
![[Pasted image 20231201014128.png]]
User/VM:
![[Pasted image 20231201014020.png]]
## Explanation
The TCP protocol requires three handshake process to build a connection. When the server requires a SYN request, it will send a SYN-ACK as a response. During this process, the server will cost computing resources while it is receiving the first SYN packet. It will cost 60 seconds to release this resource (which is why the lab notes told us to wait 1 minute). 
Both the C and Python script send plenty of SYN packets to the server, which cause the server reach the capacity soon, which is around 100 half open connections. When the server resource is exhausted, it cannot receive new connections even though they are regular requests. 
# Question 2
## 2.1 Screenshots and Results
User Machine:
![[Pasted image 20231203021519.png]]
Virtual Machine
![[Pasted image 20231203021603.png]]
Wireshark: 
![[Pasted image 20231203021657.png]]
2.2 
Attacker: 
![[Pasted image 20231203025559.png]]
User: 
![[Pasted image 20231203024834.png]]
3.1 
User Machine: 
![[Pasted image 20231203150709.png]]
Victim Machine:
![[Pasted image 20231203150935.png]]
Attacker Machine:
![[Pasted image 20231203151021.png]]
3.2 
Attacker Listening: 
![[Pasted image 20231203151722.png]]
Attacker Machine: 
![[Pasted image 20231203151808.png]]
User Machine:
![[Pasted image 20231203151850.png]]