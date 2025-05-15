## LAB - 1
**lab link: <https://portswigger.net/web-security/nosql-injection/lab-nosql-injection-detection>**

 **Topic :-** 

- Detecting NoSQL injection.

 **To Solve :-**

- Perform a NoSQL injection attack that causes the application to display unreleased products.

 **Procedure :-**

1. In the site , try to filter out product under one category.
2. Add `'` in the url , to see if it break the site, which it does means its NO_SQL vuln.
3. Now try `" ' || '1' == '1 "` , add it in the url , and you see the unreleased products.


## LAB - 2
**lab link: <https://portswigger.net/web-security/nosql-injection/lab-nosql-injection-bypass-authentication>**

 **Topic :-** 

- Exploiting NoSQL operator injection to bypass authentication.

 **To Solve :-**

- Log into the application as the `administrator` user.

 **Procedure :-**

1. Open the site in burp, login with wiener creds. open login request in repeater. and it can be seen that username and password are sent in form of json.
2. Replace the password to `{ "$ne" : "" }` , its a mongo syntax in which the site is build on, and its means not equal to `" "`, which is true , so it will login wiener.
3. Now change the username to `{ "$regex" : "^a" }`, which means username which start with "a" which should be admin and send. and response shows that you login as admin, so copy the session cookie . send a my-account request to repeater page and paste the session cookie and send. And Voila.


## LAB - 3
**lab link: <https://portswigger.net/web-security/nosql-injection/lab-nosql-injection-extract-data>**

 **Topic :-** 

- Exploiting NoSQL injection to extract data.

 **To Solve :-**

- Extract the password for the `administrator` user, then log in to their account.

 **Procedure :-**

1. Open site in burp. login with wiener creds. open get lookup request to repeater.
2. Try to change the username to administrator, and it works, but we need password.
3. So try `'` after administrator, the response shows there internal error. 
4. So try  ` '&&user.username[0]=='a ` , "user" is used as in previous responses there is user.email, and user.username[0] is `a` of administrator , it should be true, but there is an error in response. So try ` '&&this.username[0]=='a `, and this worked.
5. So try  ` '&&this.password.length=='$1$ ` , and iterate until the length of password is found, the response containing diff adn largest packet size would becoz of the correct length.
6. then iterate  ` '&&this.password[$0$]=='$a$` and the response with largest and diff packet size are the one with password chars. And then login with administrator credentials.

