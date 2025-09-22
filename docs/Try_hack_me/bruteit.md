**lab link: <https://tryhackme.com/room/bruteit>**

Scanning 

![nmap](../assets/tryhackme/brute_it/nmap.png)

Gobuster the IP...

![gobuster](../assets/tryhackme/brute_it/gobuster.png)

Got to site and view source...

![viewsite](../assets/tryhackme/brute_it/web_src.png)

Brute force the password using hydra with `rockyou.txt` ...

![hydra](../assets/tryhackme/brute_it/hydra.png)

![hydra2](../assets/tryhackme/brute_it/pass.png)

Use the creds to login, you will get the `web flag` and the `RSA private key`...

![webflag](../assets/tryhackme/brute_it/web_flag.png)

Use the `john` to crack the passphrase from key...

![userpass](../assets/tryhackme/brute_it/rsa_restore.png)

Ssh to the `john` and get the `user.txt` ...

![usertxt](../assets/tryhackme/brute_it/user_flag.png)

Use `sudo -l` and `cat` the `/etc/shadow` file...

![shadow](../assets/tryhackme/brute_it/root_pass.png)

Crack the root password using the `john` and `rockyou.txt` ...

![rootpass](../assets/tryhackme/brute_it/root_crackpass.png)

Su `root` and get the `root.txt` ...

![root](../assets/tryhackme/brute_it/root_flag.png)