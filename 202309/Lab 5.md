# Question 1 
## 1.1 Explanation
I have created a python file containing the required lines code. 
```
#!/usr/bin/env python3
from scapy.all import *
def print_pkt(pkt):
    pkt.show()
pkt = sniff(iface='br-88c7c3ba0526', filter='icmp', prn=print_pkt)

```
It can capture the bridges information. Then, we we uses the container to ping the corresponding server, the information will be retrieved by the python program. 
### Results
Command Line of running Python file: 
![[Pasted image 20231130201142.png]]
## 1.2 Explanation
Through letting the wire shark monitoring the bridge of the container, it can access all the ICMP packets the container send and receive. 

### Results
Wireshark: 
![[Pasted image 20231130201327.png]]
## 1.3 Explanation
By using the `tcpdump`, we can set the source as 10.9.0.5. Then, we can capture all the packets that container transfers. 
### Result
Command Line of running `tcpdump`: 
![[Pasted image 20231130203110.png]]

# Question 2
## Explanation
I modified the source as a not existed source, which is 123.123.123.123. Then, when I send the spoofed packet back to the container, it can be shown on the Wireshark, that there is a ICMP send packet from 123.123.123.123 to 10.9.0.5, and also a reply packet. 
## Result
Python File: 
![[Pasted image 20231130205648.png]]
Wireshark: 
![[Pasted image 20231130205751.png]]
# Question 3
## Explanation
The give Python program imports the `Scapy` lib and manage every sniffed packet `pkt`, to check if it is ICMP echo request. If so, it sends a spoofed ICMP echo response by exchange  the source address and the destination address. 
In this experiment, I changed the `iface` to the designated bridge container. 
When the container sending the `icmp` packets, it would be captured by the program. 
## Result
Command line: 
![[Pasted image 20231130211152.png]]

# Question 4
## Question 4.1
In the sniffing and then spoofing experiment in the lab, why can you get the echo reply from 1.2.3.4 which does not exist on the Internet? 
Answer: When the container send the ICMP request, the network stack originally should send the packet to the designated IP address. However, during this process, the packet is captured by the Python script. Whatever the target IP address is, the program can send the spoofed response. 
## Question 4.2
In the above experiment, why can’t you get the echo reply from 10.9.0.99?
Answer: For ARP, it is used when finding the data link level MAC address related to the network level IP address. When the host needs to connect another IP address that is within the current local network. It will send a ARP request, to find the corresponding MAC address related to the IP address. For 1.2.3.4, the packet will use the default gateway router. For 10.9.0.99, it will directly be sent to the MAC address, so that if the MAC address does not exist and does not reply to the ARP request, the program cannot capture this packet. 

# Question 5
Please conduct an investigation to explain why Wireshark is still able to sniff packets. 
Answer: Wireshark usually requires Admin level privilege to manage the packets on the network level. However, when we observe Wireshark's sub programs. We may observe there is a program called `dumpcap`. 
![[Pasted image 20231201003429.png]]
When we do a further look at the `dumpcap` file, we may observe that it has two privileges.  These privileges are special security level in Linux, called capabilities. It is used to provide necessary privilege for some programs without providing full root access. For the first one, `cap_net_raw` can allow the program access raw sockets to achieve the low level network protocol. It can send the receive the packet from network level. The second one is `cap_net_admin`. It provides the privilege for network management, such as edit the network configuration, change routers map, edit the interfaces and ARPs. 
The EIP after that means effective, inheritable and permitted. These are a part of the capabilities level we mentioned before. 
![[Pasted image 20231201003447.png]]