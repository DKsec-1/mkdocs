**lab link: <https://tryhackme.com/room/cowboyhacker>**

Scanning :

![nmap](../assets/tryhackme/bounty_hacker/nmap.png)

Login `ftp` with `anonymous` Creds and `get` all the files...

![ftp](../assets/tryhackme/bounty_hacker/ftp_get.png)

Content of files ...

![content](../assets/tryhackme/bounty_hacker/cat_getfiles.png)

They contain username and list of passwords, use `hydra` to get the password...

![hydra](../assets/tryhackme/bounty_hacker/hydra.png)

`ssh` the IP using the Creds, and get the `user.txt` and `sudo -l` to privesc and get the `root.txt` ...

![root](../assets/tryhackme/bounty_hacker/ssh.png)