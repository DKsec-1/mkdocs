## LAB - 1
**lab link: <https://portswigger.net/web-security/deserialization/exploiting/lab-deserialization-modifying-serialized-objects>**

 **Topic :-** 

- Modifying serialized objects.

 **To Solve :-**

- Edit the serialized object in the session cookie to exploit this vulnerability and gain administrative privileges. Then, delete the user `carlos`.

 **Procedure :-**

1. Login using given credentials.
2. Then check your cookie. it will be base64 bit string, convert it. then the serialized object can be seen.
3. There is an attribute of "admin" status which will be 0 for users. Convert it to 1 and then send again the packet.
4. Change the cookie "admin" to 1 till you delete the carlos.


## LAB - 2
**lab link: <https://portswigger.net/web-security/deserialization/exploiting/lab-deserialization-modifying-serialized-data-types>**

 **Topic :-** 

- Modifying serialized data types.

 **To Solve :-**

- Edit the serialized object in the session cookie to access the `administrator` account. Then, delete the user `carlos`.


 **Procedure :-**

1. Login with credentials, verify the session cookie.
2. Change the serialized query to of user "adminstrator" and access_key to interger 0.
3. After applying changes , then send request and verify if its works .
4. If works, then change the path to "/admin/delete?username=carlos".


## LAB - 3
**lab link: <https://portswigger.net/web-security/deserialization/exploiting/lab-deserialization-using-application-functionality-to-exploit-insecure-deserialization>**

 **Topic :-** 

- Using application functionality to exploit insecure deserialization.

 **To Solve :-**

- Edit the serialized object in the session cookie and use it to delete the `morale.txt` file from Carlos's home directory.

 **Procedure :-**

1. Login using credentials. And delete the account.
2. Then verify the session cookie of the POST packet.
3. Then change the "avatar_link" to the location specify in the statement "/home/carlos/morale.txt". Apply the changes and Voila.


## LAB - 4
**lab link: <https://portswigger.net/web-security/deserialization/exploiting/lab-deserialization-arbitrary-object-injection-in-php>**

 **Topic :-** 

- Arbitrary object injection in PHP.

 **To Solve :-**

- Create and inject a malicious serialized object to delete the `morale.txt` file from Carlos's home directory. You will need to obtain source code access to solve this lab.

 **Procedure :-**

1. Login through credentials, check the serialized object in the cookie session.
2. In the sitemap, there is a website reference to "CustomTemplate.php", send it to repeater and Add "~" at the end then send. It will shoe the source code. there is a magic method "destruct " , which can be invoked by making a arbitrary serialized object encoded in cookie session.
3. Create such arbitrary serialized object put it in cookie session of any packet containing it. then send and voila.


## LAB - 5
**lab link: <https://portswigger.net/web-security/deserialization/exploiting/lab-deserialization-exploiting-php-deserialization-with-a-pre-built-gadget-chain>**

 **Topic :-** 

- Exploiting PHP deserialization with a pre-built gadget chain.

 **To Solve :-**

- Identify the target framework then use a third-party tool to generate a malicious serialized object containing a remote code execution payload. Then, work out how to generate a valid signed cookie containing your malicious object. Finally, pass this into the website to delete the `morale.txt` file from Carlos's home directory.

 **Procedure :-**

1. Login through credentials, then verify session cookie, but this contain a token and sha1 hash. the token is the serialized object.
2. Create a php payload and then use "phpgcc" tool to convert payload to exploit to delete the calos from home directory.
3. Paste the encrypted in session cookie and send.