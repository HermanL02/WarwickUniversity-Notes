# Question 1
## 1.1 Results and Screenshots
### SYN Flooding using C
Victim Machine (Almost full capacity): 
![[Pasted image 20231203020856.png]]
Attacker Machine(Running the SYN attack code): 
![[Pasted image 20231203020824.png]]
Virtual Machine(Cannot build a new connection): 
![[Pasted image 20231203020736.png]]
### SYN Flooding using Python 
Attacker Machine(Running the SYN attack code): 
![[Pasted image 20231201014120.png]]
Victim Machine (Ran TCP metrics flush, and reach almost full capacity): 
![[Pasted image 20231201014128.png]]
User/VM(Cannot telnet to the victim server machine):
![[Pasted image 20231201014020.png]]
## Explanation
The TCP protocol requires three handshake process to build a connection. When the server requires a SYN request, it will send a SYN-ACK as a response. During this process, the server will cost computing resources while it is receiving the first SYN packet. It will cost 60 seconds to release this resource (which is why the lab notes told us to wait 1 minute). 
Both the C and Python script send plenty of SYN packets to the server, which cause the server reach the capacity soon, which is around 100 half open connections. When the server resource is exhausted, it cannot receive new connections even though they are regular requests. 
# Question 2
## 2.1 Screenshots and Results
### TCP RESET attack
Modified Input: 
`tcp = TCP(sport=40442, dport=23, seq=92018809, flags="R")`
User Machine(Connection stopped by attacker):
![[Pasted image 20231203021519.png]]
Attacker Machine(Running the malicious code): 
![[Pasted image 20231203021603.png]]
Wireshark(Observed parameters): 
![[Pasted image 20231203021657.png]]
### Auto TCP RESET attack
Attacker: 
![[Pasted image 20231203025559.png]]
User(Connection stopped by the attacker): 
![[Pasted image 20231203024834.png]]
## 2.2 Explanation
In the first manual attack, we need to set the parameters through what we observed in the Wireshark. We can use filters to filter the target IP and retrieve the latest TCP connection from the capture window. Therefore, we can use the TCP connection's details to fill in the Python program. 
Comparatively, the second attack is more straightforward, it sniffs the network packets from the designated bridge, then  it can automatically retrieve the above information from the packet. 
The attack can work is because that the script creates a packet by defining the source port, destination port, and sequence number. Then, it sets the flags as R, which means t his packet is a reset packet. It then sends this packet to stop the connection between the designated port and the target IP address. The server would think this RST packet is sent from the user machine, then it would think the user wants to stop the connection, then it stops the connection. 
# Question 3
## 3.1 Results and Screenshots
### Inject command
User Machine(Freeze when typing the 10th character): 
![[Pasted image 20231203150709.png]]
Victim Machine(Injected a `success` file under `tmp`):
![[Pasted image 20231203150935.png]]
Attacker Machine(Running the code):
![[Pasted image 20231203151021.png]]
### Create a reverse shell
Attacker Listening(Created a reverse shell): 
![[Pasted image 20231203151722.png]]
Attacker Machine(Running the code): 
![[Pasted image 20231203151808.png]]
User Machine(Window Freezed):
![[Pasted image 20231203151850.png]]
## 3.2 Explanation
The script sniffs the information on the designated bridge. Then it use the received data packet to get the TCP and IP information, especially for the TCP sequence and acknowledge number, which can calculate the correct sequence and acknowledge number to make the server believe that these packets are sent from the legit user.  
In the first part, it hijacks the user's session and store `success` file under the folder of `tmp`. The second one uses a reverse shell command to project the currren