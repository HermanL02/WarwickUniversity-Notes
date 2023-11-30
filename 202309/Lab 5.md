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
## Results
![[Pasted image 20231130201142.png]]
## 1.2 
![[Pasted image 20231130201327.png]]
## 1.3 
![[Pasted image 20231130203110.png]]

## 2.1 
![[Pasted image 20231130205648.png]]

![[Pasted image 20231130205751.png]]
# 3
![[Pasted image 20231130211152.png]]