# Question 1
## 1.1 Results and Screenshots
### Task 1.1
Input: 
![[Pasted image 20231116102437.png|650]]
Output: 
![[Pasted image 20231116102320.png|650]]
### Task 1.2
Input: 
![[Pasted image 20231116103500.png]]
Output: 
![[Pasted image 20231116103655.png]]
### Task 1.3
![[Pasted image 20231116103958.png]]
![[Pasted image 20231116104012.png]]
## 1.2 Explanation
### Task 1.1
The value I used is `Admin'#` as the value of 'username' input. The single quote terminates the username string and the hash comments out the rest of the SQL query, bypassing the password check. 
The reason is that as we know that the default command has two requirements in "WHERE" clause. One of them is "Username" and another is "Password". 
Therefore, to make the SQL query return the information of the designated username. We have two ways. 
	- One is to make the query ignore the password part, which we have to make the Password part as comments. 
	- Another way is to make the password is TRUE, which means we can use the 'or' statement to make password always be TRUE. 
By evaluating the efficiency of the code, I choose the first one. In the `Admin'#`,  `'` means to end the username input, and `#` means to make the rest part as comments. 
### Task 1.2
The way to think is basically the same, but due to the curl command's limitation, we can use URL enco %27 and %23 to substitute the ' sign and # sign. 
### Task 1.3
By using the professor given value, we may notice that this website is using the prepared statements method to avoid the append of new statements. 
# Question 2
## Results and Screenshots
### Task 2.1
Input: 
![[Pasted image 20231119173517.png|650]]
Output:
![[Pasted image 20231116104834.png|650]]
### Task 2.2
Input: 
![[Pasted image 20231119183249.png|650]]
Output:
![[Pasted image 20231119183437.png|650]]
### Task 2.3
Input: 
![[Pasted image 20231119184228.png]]
Output: 
The password changed from the last "...fc0" to "...10c". 
![[Pasted image 20231119183951.png|650]]
Logged in using Admin and 0. 
![[Pasted image 20231119184122.png|650]]
## Explanation of the values
### Task 2.1
I filled `', Salary = '1000000`in to the yellow blank. 
The reason is : 
`'` was used to end the previous statement, which is nickname. `,` was used to create a separation between this variable and the next variable.  
`Salary = '1000000` is used to set my salary. I left one `'` sign is because there is already a sign at the original statement. 
### Task 2.2
I filled`', Salary = '0' WHERE Name = 'Admin';#`in to the yellow blank. 
Alternative answer might work: `ID = 6` would also work, and the number in salary does not matter. 
`WHERE Name = 'Admin';#` was used to change the original ID to new Name based where condition, and used `;#` to end the statement. 
The other parts are similar to the previous question. 
### Task 2.3
`', Password = sha1('0') WHERE Name = 'Admin';#`
Password was reset to a new one based on the same encryption. 
# Question 3
## Results and Screenshots
### Admin'# Testing
Before: 
![[Pasted image 20231119191824.png]]
After: 
![[Pasted image 20231119192245.png]]
## Explanation
```
$input_uname = $_GET['username'];
$input_pwd = $_GET['Password'];
$hashed_pwd = sha1($input_pwd);
$conn = getDB();
$stmt = $conn->prepare("SELECT id, name, eid, salary, ssn FROM credential WHERE name= ? AND Password= ?");
$stmt->bind_param("ss", $input_uname, $hashed_pwd);
$stmt->execute();
$stmt->bind_result($id, $name, $eid, $salary, $ssn);
$stmt->fetch();
$stmt->close();
$conn->close();
```
Using the prepared statement can use the '?' sign as a placeholder to receive the user inputs, which means the real user inputs are separated from the query. The separation is essential for the security. 
By using the **bind_param** function, we can make sure that the user input is bind to the placeholders, and **they are not considered as SQL query, but only as data.** 
