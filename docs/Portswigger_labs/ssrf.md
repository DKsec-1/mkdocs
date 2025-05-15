## LAB - 1
**lab link: <https://portswigger.net/web-security/ssrf/lab-basic-ssrf-against-localhost>**

 **Topic :-** 

- Basic SSRF against the local server.

 **To Solve :-**

- Change the stock check URL to access the admin interface at `http://localhost/admin` and delete the user `carlos`.


 **Procedure :-**

1. Open the site in Burp-suite, try to check the stock of any product.
2. Open post stock request in repeater, there is a stock api parameter , url-decode it, it tells the sever to what to do.
3. So change the stock api parameter to `http://localhost` to see what happens at the sever local host and it. the response show there is a admin panel , try to get the path to admin panel which is `/admin` and add it on to localhost and send. in the response, there are delete function for carlos and wiener , get the path for deleting carlos which is `/admin/delete?username=carlos`, add it on the localhost again and send. And Done.


## LAB - 2
**lab link: <https://portswigger.net/web-security/ssrf/lab-basic-ssrf-against-backend-system>**

 **Topic :-** 

- Basic SSRF against another back-end system.

 **To Solve :-**

- Use the stock check functionality to scan the internal `192.168.0.X` range for an admin interface on port `8080`, then use it to delete the user `carlos`.

 **Procedure :-**

1. Open the site in Owasp-Zap, check stock of any product. 
2. Open stock request in requester tab . there url encoded stockApi parameter. change it to only `http://192.168.0.1:8080/` and then send , which returns an error missing parameter, change the ip 192.168.0.2 and send , which return error "cannot connect" and few more , all causes "cannot connect"
3. Now try to fuzz the `http://192.168.0.$x$:8080` with number from 0-255. one with the smallest response size will be the one with correct ip address. open it in requester tab and add`/admin` as suffix to the address and send. admin panel will open in response.
4. Locate the path to delete carlos from raw response and replace it to the stock Api and send again. And Done.


## LAB - 3
**lab link: <https://portswigger.net/web-security/ssrf/lab-ssrf-with-blacklist-filter>**

 **Topic :-** 

- SSRF with blacklist-based input filter.

 **To Solve :-**

- Delete the user `carlos`.

 **Procedure :-**

1. Open site in Burp-suite, try check stock function.
2. Open the post stock request to repeater.
3. Change the stockApi to `http://localhost` and send , it will be block by firewall. try `http://127.0.0.1` , which also will be blocked.
4. Then try `http://127.1/` which will resolve to `http://127.0.0.1` but will not be blocked by firewall , and send. 
5. In the response there a path to admin panel, add it to stock Api and send, it will also block by firewall, mean admin word is blacklisted also, try double url-encoding the `a` from "admin", and then send. it will bypass the firewall.
6. In response there is a path to delete `carlos` , add it to the stockApi and send . And Done.


## LAB - 4
**lab link: <https://portswigger.net/web-security/ssrf/lab-ssrf-with-whitelist-filter>**

 **Topic :-** 

- SSRF with whitelist-based input filter.

 **To Solve :-**

- Delete the user `carlos`.

 **Procedure :-**

1. Open site in Burp-suite, and try check stock function.
2. Open the post stock request in repeater, change the stockApi and try localhost or 127.0.0.1 or 127.1, they will be block, only "stock.weliketoshop.net" will be allowed.
3. So change the stockApi to `http://localhost#@stock.weliketoshop.net/`, this work as localhost as element to the site, and double url-encode the `#` to bypass it. and send.
4. In response , there is path to admin panel , add it to the stockApi and send.
5. Again in response, there is path to delete carlos, add it to the StockApi adn send. And Done.


## LAB - 5
**lab link: <https://portswigger.net/web-security/ssrf/lab-ssrf-filter-bypass-via-open-redirection>**

 **Topic :-** 

- SSRF with filter bypass via open redirection vulnerability.

 **To Solve :-**

- Delete the user `carlos`.

 **Procedure :-**

1. Open site in Burp-suite. try check stock function and next product button.
2. Open post stock request in repeater , and it can be seen that stockApi only contain path , not the ip addr. So open get product request in repeater , and see that it path is similar to that of post stock' stockApi's . So replace the stockApi's value to that of get product path's. 
3. And now change path in the value to ip address given in question and send. in response , the path to delete carlos is given , add it to stockApi and send. And Done.