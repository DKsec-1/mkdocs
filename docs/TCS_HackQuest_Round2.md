` These write-ups are little-bit based on memory due to time constraints during the event. `

## 1. Shade Wars

Solution :

A PNG file named ` Shade Wars ` is given.

The main objective is to convert only the white background of the image to the black, which can be done by visiting the site <https://onlinepngtools.com/change-png-color> and convert colors.

![shade_wars_1](assets/TCS_Hackquest_2/Shade_war_1.PNG)

Then scan the recieved QR code using <https://scanqr.org/> site to get the hidden flag key.

![shade_wars_2](assets/TCS_Hackquest_2/shade_wars_2.PNG)


## 2. Tolkien's Secret

Solution :

A website is given, and as the name suggest there is something to do with ` token and cookie `.

So open the site in ` burpsuite `. Reload the site, to create the initial cookies. It seems it is the JSON web token. 

![tolkiens_secret_1](assets/TCS_Hackquest_2/tolkeins_secret_1.PNG)


![tolkiens_secret_2](assets/TCS_Hackquest_2/tolkeins_secret_2.PNG)

Then take the payload part of the jwt and decode it using base64. there is a ` role ` in token which is initially set to ` guest `, convert it to ` admin `. then send the packet. 

![tolkiens_secret_3](assets/TCS_Hackquest_2/tolkeins_secret_3.PNG)


![tolkiens_secret_4](assets/TCS_Hackquest_2/tolkeins_secret_4.PNG)

In respone the hidden flag key is visible.


![tolkiens_secret_5](assets/TCS_Hackquest_2/tolkeins_secret_5.PNG)


## 3. Veil of Void

Solution :

A PDF named ` Veil of Void_BabaBreach_ASSGNMNT_PT_REPORT ` is given which is locked under a password. upload it to <https://www.lostmypass.com/file-types/pdf/> to crack the pdf and get the password ` secret `.

![veil_of_void_1](assets/TCS_Hackquest_2/Veil_of_void_1.PNG)

Then open the pdf using the received password. after thoroughly reading the pdf. there is a highlight at ` page 25 ` which clearly show the hidden flag key.


![veil_of_void_2](assets/TCS_Hackquest_2/Veil_of_void_2.PNG)