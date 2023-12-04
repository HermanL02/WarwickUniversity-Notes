# Question 1: Background
## Diagram
![[Drawing 2023-11-22 21.38.46.excalidraw|650]]
## Explanation
Buffer overflow occurs when the program writes data to a buffer that exceeds its capacity, and when it overwrites the adjacent area, it will have a buffer overflow. This vulnerability can allow the attackers to inject malicious code to the area that usually does not allow code to run. The program's return address and the previous frame pointer can be overwritten, which may allow the attacker to execute the code redirect to the injected malicious code, which may allow the attacker to control and damage the computer system. 
# Question 1
## Screenshots
![[Pasted image 20231202152652.png]]
![[Pasted image 20231204144745.png]]

Question 2
`ret = 0xffffd158 + 300 + 4 + 4; S = 60`
![[Pasted image 20231204192015.png]]