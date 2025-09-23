**lab link: <https://tryhackme.com/room/yearoftherabbit>**

Scanning :

![nmap](../assets/tryhackme/yearoftherabbit/nmap.png)

Gobuster the site to find the hidden directory, you will find the `/sup3r_s3cr3t_fl4g.php`...

![secretphp](../assets/tryhackme/yearoftherabbit/secretphp.png)

Another hidden page, disable the javascript and go to that page...

![hiddendir](../assets/tryhackme/yearoftherabbit/hiddendir.png)

there will a png file download it, and there will be username and password list...

![userpass](../assets/tryhackme/yearoftherabbit/userpass.png)

Use the hydra to crack the password for `ftpuser`...

![crack](../assets/tryhackme/yearoftherabbit/passcrack.png)

Use the Creds to ftp to the ip...

![ftp](../assets/tryhackme/yearoftherabbit/ftp.png)

Get the file, which will contain the Brainfuck code, Decode it...

![elicred](../assets/tryhackme/yearoftherabbit/elicred.png)

Use the Creds to ssh the ip...

![ssh](../assets/tryhackme/yearoftherabbit/elissh.png)

You will find a leet text `s3cr3t`, try find it...

![find](../assets/tryhackme/yearoftherabbit/gwendolinepass.png)

You will get the `gwendonline` password, so Su in it and get the `user.txt`...

![user](../assets/tryhackme/yearoftherabbit/user_txt.png)

Then use `sudo -l` to see the sudo priviledges, and gtfobin it...

![priv1](../assets/tryhackme/yearoftherabbit/privesc1.png)

and add `:!/bin/bash` at last...

![priv2](../assets/tryhackme/yearoftherabbit/privesc2.png)

And Voila, you will get the root, so get the `root.txt` ...

![root](../assets/tryhackme/yearoftherabbit/rootflag.png)