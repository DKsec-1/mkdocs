## LAB - 1
**lab link: <https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-excessive-trust-in-client-side-controls>**

 **Topic :-** 

- Excessive trust in client-side controls.

 **To Solve :-**

- Buy a "Lightweight l33t leather jacket".

 **Procedure :-**

1. Open site in burp suite , login with given creds.
2. Add to cart the required product.
3. Open cart page, when checkout it says insufficient credits. remove the product from cart.
4. Open the cart request in repeater, change the price to less than 1 and send.
5. Then open cart page , it can be seen that the product is added with less price. then checkout.


## LAB - 2
**lab link: <https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-high-level>**

 **Topic :-** 

- High-level logic vulnerability.

 **To Solve :-**

- Buy a "Lightweight l33t leather jacket".

 **Procedure :-**

1. Open the site in Burp-suite, login with given creds. add the jacket in cart. open cart page and try to check out , it shows insufficient credits.
2. Send the post cart request to the repeater, here you can put negative value in quantity, which makes the total price negative-> try to check -> it show an error that price should not be zero or less than zero.
3. So add an other product to the cart having value less then the jacket, then send its post cart request to repeater and puts its quantity in negative as such that the total value becomes less than 100.and then checkout.


## LAB - 3
**lab link: <https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-inconsistent-security-controls>**

 **Topic :-** 

- Inconsistent security controls.

 **To Solve :-**

- Access the admin panel and delete the user `carlos`.

 **Procedure :-**

1. Register an account . verify email. login with the credentials.
2. Update the email to an @dontwannacry domain.
3. Then open admin panel and delete carlos.


## LAB - 4
**lab link: <https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-flawed-enforcement-of-business-rules>**

 **Topic :-** 

- Flawed enforcement of business rules.

 **To Solve :-**

- Buy a "Lightweight l33t leather jacket".

 **Procedure :-**

1. Login with credentials -> try to buy jacket -> insufficient credits.
2. Apply the "NEWCUST5" coupon, it reduces the price by 5 . try to apply it again , return an error "applied already".
3. Go to home page , signup for newsletter. you will get "SIGNUP30" coupon. 
4. Apply the "SIGNUP30" coupon, it reduces the the price by 30%, try to apply it again, same error "applied already".
5. But try to apply "NEWCUST5" just apply "SIGNUP30", it will not return any error. apply the both coupon alternatively , till the total price become less than your credits. and then checkout.


## LAB - 5
**lab link: <https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-low-level>**

 **Topic :-** 

- Low-level logic flaw.

 **To Solve :-**

- Buy a "Lightweight l33t leather jacket".

 **Procedure :-**

1. Open site in Owasp-Zap -> login with credentials in site -> try buy leather jacket -> insufficient credits.
2. Open the post cart request in requester tab, then change quantity to find the highest number we can add at a time, that would be 99.
3. Fuzz this request with null to increase the total cost to get to negative value and eventually to reach btw 1237 to 100. then another product and increase its quantity to reach the total cost btw 0 to 100. then checkout.


## LAB - 6
**lab link: <https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-inconsistent-handling-of-exceptional-input>**

 **Topic :-** 

- Inconsistent handling of exceptional input.

 **To Solve :-**

- Access the admin panel and delete the user `carlos`.

 **Procedure :-**

1. Open site in burp suite, its says you have to be @dontwannacry user. try to register with given email, which can be seen after verification in my account page.
2. Open that register request in intruder , see how the site behave when you put large value in email. use char block with A and go through 100 to 500 with 100 per step, all the value of A are prefixed to the given email . all go through and can be seen in emails, open the latest one which should contain 500 A, but after verification, in my-acc page only 255 A can be seen and rest are truncated.
3. So we can try that at registering it contain the given email but after verification ,in my-acc page it only remains with @dontwannacry.
4. Try register again as csrf token refresh. then send post register request to repeater, replace the email to the 238 A + @dontwannacry + given email, then send. verify the mail. then login creds in my-acc , where it can be seen as @dontwannacry domain email and there is an amin panel , go ther and delete carlos.

`here As are not any particular, you can use any letter and should be different if gone wrong at some place as mail should be different at every register number, A or any other letter are important.`


## LAB - 7
**lab link: <https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-weak-isolation-on-dual-use-endpoint>**

 **Topic :-** 

- Weak isolation on dual-use endpoint.

 **To Solve :-**

- Access the `administrator` account and delete the user `carlos`.

 **Procedure :-**

1. Open site in Burp-suite, login with credentials in site. try changing email and investigate the request in burp nothings there.
2. Try changing password , and open post change-password request in repeater . change username to administrator and send, it show incorrect password error. then remove the current-password parameter and send; and its successful.
3. login with `administrator` and new password. then delete the `carlos`


## LAB - 8
**lab link: <https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-insufficient-workflow-validation>**

 **Topic :-** 

- Insufficient workflow validation

 **To Solve :-**

- Buy a "Lightweight l33t leather jacket".

 **Procedure :-**

1. Open site in Burp-suite , login with credentials. try to buy jacket , it show insufficient credits.
2. Try with any thing cheaper than 100 . and compare the flow in both in burp.
3. With jacket , add to cart -> checkout -> insufficient funds.
4. With cheaper thing, add to cart -> checkout -> order-confirmation.
5. So try to change to flow in burp and browser intercepted by burp, go to leather jacker page -> add to cart -> open cart page -> send the order-confirmation packet to repeater and send it. And done , order is placed.