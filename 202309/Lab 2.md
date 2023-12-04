# Question 1: Background
## Diagram
![[Drawing 2023-11-22 21.38.46.excalidraw|650|650]]
## Explanation
Buffer overflow occurs when the program writes data to a buffer that exceeds its capacity, and when it overwrites the adjacent area, it will have a buffer overflow. This vulnerability can allow the attackers to inject malicious code to the area that usually does not allow code to run. The program's return address and the previous frame pointer can be overwritten, which may allow the attacker to execute the code redirect to the injected malicious code, which may allow the attacker to control and damage the computer system. 
# Question 2
## Question 2.1 
### Screenshots
#### Task 1.1
![[Pasted image 20231202152652.png|650]]
#### Task 1.2
![[Pasted image 20231204144745.png|650]]
### Explanation of result
`Note: I used exploit.py in the seed lab instead of exploit-L1.py. `

The Python script creates a `badfile`, which uses the buffer overflow vulnerability. It includes a payload and manipulate the vulnerable program's memory stack to run the shell code. The payload is full of NOP (0x90), which is used to create an area and safely execute the shellcode.  The `start` variable is used to calculate where the payload starts the shellcode. 

While it is running, the first one will echo the string "success", while the second task will create a reverse shell to connect back to the attacker computer's 10.9.0.1 with port 7070. 
## Question 2.2 Explanation of values
In the X86 system, when a function is called, the stack frame will do the following operation.. It will push the return address into the stack, and the caller's EBP will be pushed to the stack, and the new EBP value is on the top of the EBP. Therefore, the return address could be set as `EBP+8`, where the current function's EBP saves the last function's frame address, and above the EBP, is the original EBP, which is 4 bytes, and above the original `ebp`, is the current return address we want. 
We need to know the offset to precisely return the address. Therefore, we may notice that `ebp - buffer address` is the distance from the current function's `ebp` to start position of the buffer. Also, we need to consider the `ebp`'s size, which is 4 bytes, therefore, we need to `+4` to get the real offset. 

# Question 3
## Question 3.1 
### Screenshots
`ret = 0xffffd158 + 300 + 4 + 4; S = 60`
![[Pasted image 20231204192015.png|650]]
### Explanation
This task's result is similar to the previous one. The script is also to create a `badfile`. When the `badfile` is used to attack the vulnerable programs, the program's execution is redirected to the shellcode at the end of buffer. 
## Explanation
In our case, we have a maximum 300 bytes buffer area. By using our previous PowerPoint information, we understand that for a 100 bytes buffer area, the complier usually add 200 