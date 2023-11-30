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
![[Pasted image 20231130201142.png]]
## 1.2 Explanation
Through letting the wire shark monitoring the bridge of the container, it can access all the ICMP packets the container send and receive. 

### Results
![[Pasted image 20231130201327.png]]
## 1.3 Explanation
By using the tcpdump, we can set the source as 10.9.0.5. Then, we can capture all the packets that container transfers. 
### Result
![[Pasted image 20231130203110.png]]

# Question 2
## Explanation

## Result
![[Pasted image 20231130205648.png]]

![[Pasted image 20231130205751.png]]
# 3
![[Pasted image 20231130211152.png]]