## Brooklyn Nine Nine
**lab link: <https://tryhackme.com/room/brooklynninenine>**

Scanning 

![nmap](../assets/tryhackme/agent_sudo/nmap.png)

Go to the http link, Open the site through Burp suite, in the "User-agent" header replace default value with "R" as hinted in web page. 

![useragent](../assets/tryhackme/agent_sudo/user-agent.png)

it shows there are 25 members but there is 26 alphabets, so one contain some info, So enumerate through all alphabets, and in C, you get the username...

![Useragent_c](../assets/tryhackme/agent_sudo/uagent_c.png)

Then use Hydra to crack ftp password of "Chris"...

![hydra](../assets/tryhackme/agent_sudo/hydra_ftp.png)

Then get all the files from ftp...

![get_files](../assets/tryhackme/agent_sudo/get_files.png)

the contents are as follows...

![files](../assets/tryhackme/agent_sudo/files.png)

Crack the passwords and Unzip the zip file...

![unzip](../assets/tryhackme/agent_sudo/unzip_zip.png)

Decode the the passphrase and get password...

![ssh](../assets/tryhackme/agent_sudo/decode.png)

Then ssh to James, and get the User.txt...

![ssh](../assets/tryhackme/agent_sudo/ssh_james.png)

And use "sudo -l" and gtfobin to get the root access, and get the Root.txt...

![root](../assets/tryhackme/agent_sudo/root.png)