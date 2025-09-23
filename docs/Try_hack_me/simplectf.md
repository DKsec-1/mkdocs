**lab link: <https://tryhackme.com/room/easyctf>**

Scanning :

![nmap](../assets/tryhackme/simple_ctf/nmap_normal.png)

Directory enumeration the IP...

![dir](../assets/tryhackme/simple_ctf/dirsearch.png)

Go to `simple` page...

![simple](../assets/tryhackme/simple_ctf/website_simple.png)

There is outdated version of `CMS made simple` used, search for the `CVE` for that...

![cve](../assets/tryhackme/simple_ctf/cve_exploit.png)

Use the `CVE` exploit to get the Creds and ssh to the user, and get the `user.txt`...

![user](../assets/tryhackme/simple_ctf/user_txt.png)

Now `sudo -l` to get the sudo commands...

![sudo](../assets/tryhackme/simple_ctf/vim_exp.png)

Go to `gtfobin` to find the privesc payload for `vim` ...

![gtfo](../assets/tryhackme/simple_ctf/vim_gtfo.png)

Get the root, and the `root.txt` ...

![root](../assets/tryhackme/simple_ctf/final_flag.png)