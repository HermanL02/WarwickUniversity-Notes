# Background
## What is XSS attack?
![[Drawing 2023-11-20 15.57.56.excalidraw|650]]
## Countermeasures
1. Sanitize(Filter): The goal for this countermeasure is to remove the code from user's inputs. Usually, the malicious code are embedded with a script tag. Therefore, by deleting this tag, the malicious code can be treated as normal text. 
2. Encoding: Similar to the first method, we can use the ASCII characters to treat the tag brackets '<' and '>' as characters by encoding them. It can also make the malicious code be text. 
3. Content Security Policy: This is a method to control the script usage of the files. For example, we can only allow the website use the same source script. We can also restrict the inline script with nonces to prevent users from using unknown source scripts. 
# Task 1
## Results and Screenshots
![[Pasted image 20231120123001.png|650]]
## Explanation
For the website input, it has a "Edit HTML" button which allows the users to input the HTML tags directly without sanitizing them. Therefore, if we put script tags inside the input box, the website will put everything into the database as the script tag, a`<script>alert('xss')</script>` 
