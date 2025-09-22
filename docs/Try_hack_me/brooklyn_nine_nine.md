**lab link: <https://tryhackme.com/room/brooklynninenine>**

Scanning 


![nmap](../assets/tryhackme/brooklyn_nine_nine/nmap.png)

There is Open FTP port. Try it...

![ftp](../assets/tryhackme/brooklyn_nine_nine/ftp.png)

there is `jake` which seems as username. try it with hydra to crack password...

![hydra](../assets/tryhackme/brooklyn_nine_nine/hydra.png)

We get the password, ssh the user and get the `user.txt`...

![ssh](../assets/tryhackme/brooklyn_nine_nine/user.txt.png)

then Use `Sudo -l` , you will see the `less` command , so use `!/sh` as this has `sh`...

![sh](../assets/tryhackme/brooklyn_nine_nine/sh.png)

You will get the root, traverse to the `root.txt` ...

![root](../assets/tryhackme/brooklyn_nine_nine/before_after_sh.png)