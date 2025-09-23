**lab link: <https://tryhackme.com/room/lianyu>**

Scanning :

![nmap](../assets/tryhackme/lian_yun/nmap.png)

Gobuster the IP...

![island](../assets/tryhackme/lian_yun/gobuster_island.png)

Go to the `island` page ...

![vigilante](../assets/tryhackme/lian_yun/creds_1.png)

You will get the code word or username, now again gobuster further...

![2100](../assets/tryhackme/lian_yun/gobuster_2100.png)

Go to `2100`page, in src it says that our `.ticket` file is available so again gobuster further with `ticket` extention...

![ticket](../assets/tryhackme/lian_yun/gobuster_arrow.png)

`Wget` the file and `cat` it...

![green](../assets/tryhackme/lian_yun/green_arrow.png)

Decode the code...

![decode](../assets/tryhackme/lian_yun/pass.png)

You will get the password, use that to `ftp` the IP and `get` all the files...

![ftp](../assets/tryhackme/lian_yun/files.png)

Fix the magic bytes of `Leave_me_alone.png` ...

![magicbyte](../assets/tryhackme/lian_yun/leave_mealone.png)

Now open the png, but there is not much...

![image](../assets/tryhackme/lian_yun/leave_mealone_pass.png)

Now try to extract password from the `aa.jpg` using `steghide` ...

![pass](../assets/tryhackme/lian_yun/sshpass.png)

Now you get the password, for username, there is another user while in ftp...

![otheruser](../assets/tryhackme/lian_yun/slade.png)

ssh to the IP using the Creds and get `user.txt` ...

![user](../assets/tryhackme/lian_yun/user_flag.png)

Now `sudo -l` to get sudo commands, and use the privesc payload to become root and get the `root.txt` ...

![root](../assets/tryhackme/lian_yun/root_flag.png)