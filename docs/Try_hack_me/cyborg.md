**lab link: <https://tryhackme.com/room/cyborgt8>**

Scanning :

![nmap](../assets/tryhackme/cyborg/nmap.png)

gobuster the site and go to `/etc/squid/passwd` page...

![page](../assets/tryhackme/cyborg/creds.png)

Use `hashcat` with `rockyou.txt` to decrypt password...

![hash](../assets/tryhackme/cyborg/password.png)

Go to `Admin` page and download `Archive.tar`, and try `Borg` to extract `final_archive` ...

![borg](../assets/tryhackme/cyborg/borg.png)

And `find` the `.txt` files to get any secret files...

![secret](../assets/tryhackme/cyborg/creds_ssh.png)

You will find the `ssh` Creds, login to `ssh` and get the `user.txt`...

![user](../assets/tryhackme/cyborg/user_text.png)

Use `sudo -l` to find sudo commands...

![sudo](../assets/tryhackme/cyborg/sudo%20-l.png)

append payload in `backup.sh` file...

![backup](../assets/tryhackme/cyborg/at_last_of_code.png)

Use `backup.sh` to read the `root.txt`...

![root](../assets/tryhackme/cyborg/root_txt.png)

