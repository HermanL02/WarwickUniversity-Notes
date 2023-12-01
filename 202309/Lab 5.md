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
By using the tcpdump, we can set the source as 10.9.0.5. Then, we can capture all the packets that container transfers. 
### Result
Command Line of running tcpdump: 
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
The give Python program imports the Scapy lib and manage every sniffed packet pkt, to check if it is ICMP echo request. If so, it sends a spoofed ICMP echo response by exchange  the source address and the destination address. 
In this experiment, I changed the iface to the designated bridge container. 

When the con
## Result
Command line: 
![[Pasted image 20231130211152.png]]