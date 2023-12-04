# Question 1: Background
## Diagram
![[Drawing 2023-11-22 21.38.46.excalidraw|650]]
## Explanation
Buffer overflow occurs when the program writes data to a buffer that exceeds its capacity, and when it overwrites the adjacent area, it will have a buffer overflow. This vulnerability can allow the attackers to inject malicious code to the area that usually does not allow code to run. The program's return address and the previous frame pointer can be overwritten, which may allow the attacker to execute the code redirect to the injected malicious code, which may allow the attacker to control and damage the computer system. 
# Question 2
## Question 2.1 
### Screenshots
#### Task 1.1
![[Pasted image 20231202152652.png]]
#### Task 1.2
![[Pasted image 20231204144745.png]]
### Explanation
The result of Task 1.1 shows that by using the badfile, we can inject the malicious shell code into the server. The result of Task 1.2 shows that a reverse shell is already connected to the 10.9.0.1 7070. 
## Explanation
In the X86 system, when a function is called, the stack frame will do the following operation.. It will push the return address into the stack, and the caller's EBP will be pushed to the stack, and the new EBP value is on the top of the EBP. Therefore, the return address could be set as `EBP+8`, where the current function's EBP saves the last function's frame address, and above the EBP, is the original EBP, which is 4 bytes, and above the original `ebp`, is the current return address we want. 
We need to know the offset to precisely return the address. Therefore, we may notice that `ebp - buffer address` is the distance from the current function's `ebp` to start position of the buffer. Also, we need to consider the `ebp`'s size, therefore, we need to `+4` to get the final result. 

# Question 3
`ret = 0xffffd158 + 300 + 4 + 4; S = 60`
![[Pasted image 20231204192015.png]]