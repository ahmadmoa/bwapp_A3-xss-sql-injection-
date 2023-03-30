# XSS - Reflected (AJAX/XML)
first trying my simple paylod to test ss>"S
i notes that evrey time i pass a "<" the web site  blooked  me of typing so i encode it 
and use the paylod &lt;img src=x onerror=alert('1')>;



# XSS - Reflected (Back Button)
i know  that the go back is depends on referer header so i caputre the request before going to the task and tryed to change in the button on click 
the paylod used # ">s'<script>alert(1)</script><'t'


# XSS - Reflected (Custom Header)
 isee that there is a header named bWAPP 
 so i thry to se what that do and i discovere its a field i can write the paylod in so i add the
  bWAPP:<script>alert(1)</script>
  to the headers and forward it 

# XSS - Reflected (Eval)

i see in the url there is a variable date the take a functoin so i give pass a alert fun xD 



#  - Cross Site Scripting - Reflected (POST)

1- as we see there is two input fields so i tried to enter first name and last name to see what is the behavior of the webpage and it was as follow 
Welcome first name last name
![[Pasted image 20230329205329.png]]
2-trying to leave one of required fiels empty to see the response and 
the response was that is invalid input
![[Pasted image 20230329205400.png]]
3-trying my simple paylod to test ss>"S to see if it will printed direct
	and yes it get printed
	![[Pasted image 20230329205447.png]] 
4 - inject the paylod <script>alert(1)</script> in any input field and will pop up an alert 



# XSS - Reflected (HREF)
1- as we see there is  input fields so i tried to enter a name to see  what is the behavior of the webpage and it was as follow![[Pasted image 20230329220304.png]]2 -after searching about  HREF stands for Hypertext Reference, and it is an HTML attribute used to create a hyperlink. The HREF attribute is added to an HTML anchor tag (`<a>`) to specify the destination of the link my text entered the href
3-  so first i will close the <a> tag then inject the paylod 

## XSS - Stored (Cookies)
1- trying like button what is the behavior of the webpage and it show that 
"Thank you for making your choice!"
2 -so i will intercept the request using burpsuite to see the back view 
3- anter capturing i got http request and can see the cookie header 
4- trying to change  the type of movie and and add a new type and it reflected sucessfully

# SQLiteManager XSS
so as the hint tells the virsion of sqllite manager is 1.2.4 wish is has Multiple cross-site scripting (XSS) vulnerabilities
i will try one 
1- open the SQLiteManager 
2- going to +trigger 
3- add name and in the step form inject paylod <script>alert(1)</script>
and as you can see i can execute the script 

# SQL Injection (POST/Select)
1- check the source code and find the select query with out any hiding
so UNION with the number of the movie i can access the hole table schema

SQL Injection (CAPTCHA)
after passing the capatcha trying to search for a move 
noticing that in url there is title ="the search word"
first try to select the version of database and the user 'union+all+select 1,user(), @@version,4,5,6,7'
but gives me an Error: The used SELECT statements have a different number of columns 
so tryid to select more number of columns 
 'union+all+select 1,user(), @@version,4,5,6,7'
 and its work 

# SQL Injection (SQLite)
after searching about sqlite the is a bulit in table named sqlite_master that contains metadata about the database
so using the statment to selects the names of all tabels in the sqlite database 
1'UNION%20 SELECT null,name ,null,null,null,null from sqlite_master where type ='table';
By specifying "type ='table'", the query only returns information about tables.

# SQL Injection - Blind - Time-Based
as we se there is no sign to tell you if the query is executed or what 
so first trying ' or 1=1 
The single quote at the beginning is used to close the original SQL query string.
   The `or 1=1` is a logical condition that is always true, effectively ignoring any previous conditions
nothing change 

"sleep(0.5)" is a database function that causes the database to pause for 0.5 seconds and this is a time delay to check if the query executed 
# '#'symbol is used to comment out the rest of the original SQL query 
trying ' or 1=1 AND sleep(0.5)#  and the web page paused for 0.5 seconds so there is a sql injection can happens 
