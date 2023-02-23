- Get all the info of your operating system
````
hostnamectl
````
- Get the content of a .sh:
````
file file.sh
````
- Get the PATH:
````
echo $PATH
````
- Get the bash functions available:
````
declare -F
````
- To count the results:
````
declare -f | wc -l
````
- List a function definition:
````
type quote
````
- Use a funtion:
````
quote bob
````
- If you don't have Internet, try this:
````
sudo ifconfig eth0 up
sudo dhclient eth0
````
- How to stabilise a shell:
````
python -c "import pty; pty.spawn('/bin/bash')" 
````
- SUID:
	- Files with the SUID bit set when executed are run with the permissions of the owner of the file. So if there is an binary that is owned by root and it has the SUID bit set we could theoretically use this binary to elevate our permissions.

		To find SUID binaries, we can run the following command:
```
find / -user root -perm /4000 2>/dev/null
```
- How to find any file:
```
find / type f -iname filename.txt 2> /dev/null
```
- Get the size of a file:
````
du -sh file.txt
````
- ASCII text signature Generator -> http://www.kammerl.de/ascii/AsciiSignature.php
- BASH math -> https://phoenixnap.com/kb/bash-math
- `ERROR: Unable to negotiate with X.X.X.X port 22: no matching host key type found. Their offer: ssh-rsa,ssh-dss`
````
ssh -oHostKeyAlgorithms=+ssh-dss username@x.x.x.x
````
- To encrypt an external or internal hard drive or USB:
````
sudo apt-get install cryptsetup
sudo apt-get install gnome-disk-utility
````
- Compare the size of two remote files using ssh:
````
ls -l file.txt | awk '{ print $x }' #x is the option you want
````
- How to remove a package on linux:
````
sudo apt-get remove package
````
---
# ==How to understand the /etc/passwd file in Linux==
The _/etc/passwd_ file stores vital information (described below) about users such as username, home directory, etc.

Since this file contains vital information for all users, it has reading permissions and it is not necessary to have privileges to see it.

You can read the /etc/passwd file by using the **_less_** command followed by the path as shown below.

less /etc/passwd

![](https://linuxhint.com/wp-content/uploads/2022/07/word-image-191728-1.png)
Let’s take the first two lines to explain the structure of the _/etc/passwd_ file in the following table:

|  **root** | x | 0 | 0 | root | /root | /bin/bash | 
| ----------- | ----------- |  ----------- | ----------- | ----------- | ----------- | ----------- |
|  **daemon** | x | 1 | 1 | daemon | /usr/bin | /usr/sbin/nologin |
|  USER | AUTH | UID | GID | GECOS | HOME | SHELL |

The first two rows contain the same data shown in the first two lines of the _/etc/passwd_ in the image above. It is important to note that each item is separated by two dots; you can consider the two dots as columns.

The meaning of each column is:

-   **USER:** The first field shows the username.
-   **AUTHENTICATION:** The second field shows the password status, if an x, the password is stored in the /etc/shadow file, if an
-   **UID:** The third field shows the user ID.
-   **GID:** The fourth field shows the group ID.
-   **GECOS:** This field stores user information such as full name, phone number, and email.
-   **HOME:** This field contains the path to the home directory.
-   **SHELL:** Finally, the last field shows the shell for the user.

The **_x_** in the second field indicates the password is encrypted and stored in the _/etc/shadow_ file. This file is protected by permissions and can only be read by privileged users. If instead of an X you see an asterix (*****) or exclamation mark (**!**), it means that the password is blank and the user does not need a password to login.

The user ID 0 is reserved for the root user. IDs bigger than 500 can be assigned to users. Below 500 IDs are reserved for the system.

In the following figure you can see the _linuxhintuser_ line including some GECOS information such as full name (Linux Hint) and phone numbers:
![](https://linuxhint.com/wp-content/uploads/2022/07/word-image-191728-2.png)

Years ago, passwords were stored in the _/etc/passwd_ file. this was changed. Passwords are now stored in the _/etc/shadow_ file which needs privileges.

The _/etc/passwd_ file is accessible to every user because it holds information users need to interact with the system, for example, to login.

## **How to edit the _/etc/passwd_ file**

The _/etc/passwd_ can be edited using the **_vipw_** command. This command is also useful to edit _/etc/shadow_ (When used with the _-s_ flag) and _/etc/group_ files.

To edit the _/etc/passwd_ file, run the [vipw](https://linux.die.net/man/8/vipw) command and when asked, select the text editor of your preference. In my case I’m selecting nano as shown below.

sudo vipw

![](https://linuxhint.com/wp-content/uploads/2022/07/word-image-191728-3.png)

As you can see in the following figure, after running the **_vipw_** command, the /etc/passwd file will be opened with a text editor. You can then edit all fields.

![](https://linuxhint.com/wp-content/uploads/2022/07/word-image-191728-4.png)

In the example below I will edit the _linuxhintuser_ information (Last line). As you can see, the full name is _Linux Hint_, phone numbers are _342342_ and _234234_.

![](https://linuxhint.com/wp-content/uploads/2022/07/word-image-191728-5.png)

As shown in the example below, I edited the full name, replacing the full name (_linuxhintuser_) with “_New Full Name_” and editing phone numbers.

Once you are done editing the file, close and save changes.

![](https://linuxhint.com/wp-content/uploads/2022/07/word-image-191728-6.png)

After closing and saving the file, you will be warned about possible changes you may need to reproduce in the _/etc/shadow_ file. This is not necessary if you don’t edit the password.

![](https://linuxhint.com/wp-content/uploads/2022/07/word-image-191728-7.png)

You can check the _/etc/passwd_ file using the _less_ or _cat_ commands and you will see changes were properly applied.

![](https://linuxhint.com/wp-content/uploads/2022/07/word-image-191728-8.png)

Additional functions for the _vipw_ command can be implemented using flags:

-   **-g:** The -g flag is used to edit the /etc/group file containing information about user groups.
-   **-s:** This flag is used to edit both the /etc/shadow and /etc/gshadow files.
-   **-p:** The -p flag is used to edit the passwd database.
-   **-h:** This flag is used to display the help menu.

As you can see in the content above, the _/etc/passwd_ is linked to other files like /etc/shadow and /etc/group, both of which are described below.

## **The /etc/shadow file**

As said previously, formerly Linux/Unix passwords were stored in the _/etc/passwd_ file, which was dangerous since every user has access to it. A user with access to the encrypted password can easily break it by using one of the online databases or through [brute force](https://linuxhint.com/bruteforce_ssh_ftp/).

To solve this exposure, the /etc/shadow file was implemented to store user encrypted passwords without reading permissions or without super user privileges.

You can see the _/etc/shadow_ file by using _cat_ or _less_ commands as _root_ or with _sudo_ as shown previously.

less /etc/shadow

![](https://linuxhint.com/wp-content/uploads/2022/07/word-image-191728-9.png)

As you can see in the screenshot below, there are 9 columns (Defined by two dots each). Each field contains the first information:

-   **1:** Username.
-   **2:** Encrypted password.
-   **3:** Last password change in days, counting from Jan, 1970.
-   **4:** Minimum days a user can keep a password before changing it.
-   **5:** Maximum days a user can keep a password before changing it (If 99999, then no limit)
-   **6:** In this field the root can define when a user will be requested to change the password.
-   **7:** This field shows when an account will be inactive after password expiration.
-   **8:** Password expiration date (Counting from 1 Jan, 1970).
-   **9:** The last field is reserved without containing useful information.

![](https://linuxhint.com/wp-content/uploads/2022/07/word-image-191728-10.png)

As you can see, the /etc/shadow file only contains password related information.

To change a password within this file, you need to execute the _passwd_ command followed by the username whose password you want to replace, as shown in the figure below where the _linuxhintuser_ password is updated.

sudo passwd linuxhintuser

![](https://linuxhint.com/wp-content/uploads/2022/07/word-image-191728-11.png)

As you can see above, the password was successfully changed.

## **The /etc/group file**

The /etc/group file stores information on groups. This file, like both _/etc/passwd_ and _/etc/shadow, also_ can be edited with the _vipw_ command.

You can read the _/etc/group_ file using the less command as done before.

less /etc/group

![](https://linuxhint.com/wp-content/uploads/2022/07/word-image-191728-12.png)

The file looks like the following screenshot, containing 4 columns with group related information, where the first field is group name, the second field is password related, the third is the GID (Group ID) and the fourth shows the group users.

![](https://linuxhint.com/wp-content/uploads/2022/07/word-image-191728-13.png)

I also would recommend studying the _usermode_ command, some examples are available at [https://linuxhint.com/sudo_linux/](https://linuxhint.com/sudo_linux/), also related to user administration. This command is also recommended by the _passwd_ command man page.

---
- How to upload files remotely via sftp:
```
sshpass -p passwd sftp -oHostKeyAlgorithms=+ssh-dss  username@host
put -r directory_from directory_to
```
---
# Complete list of HTTP Status Codes
### Status code 	Meaning
1xx Informational 	 
100 	Continue
101 	Switching protocols
102 	Processing
103 	Early Hints
  	 
2xx Succesful 	 
200 	OK
201 	Created
202 	Accepted
203  	Non-Authoritative Information
204 	No Content
205 	Reset Content
206 	Partial Content
207 	Multi-Status
208 	Already Reported
226 	IM Used
303 	See Other
304 	Not Modified
305 	Use Proxy
306 	Switch Proxy
307 	Temporary Redirect
308 	Permanent Redirect
  	 
4xx Client Error 	 
400 	Bad Request
401 	Unauthorized
402 	Payment Required
403 	Forbidden
404 	Not Found
405 	Method Not Allowed
406 	Not Acceptable
407 	Proxy Authentication Required
408 	Request Timeout
409 	Conflict
410 	Gone
411 	Length Required
412 	Precondition Failed
413 	Payload Too Large
414 	URI Too Long
415 	Unsupported Media Type
416 	Range Not Satisfiable
417 	Expectation Failed
418 	I'm a Teapot
421 	Misdirected Request
422 	Unprocessable Entity
423 	Locked
424 	Failed Dependency
425 	Too Early
426 	Upgrade Required
428 	Precondition Required
429 	Too Many Requests
431 	Request Header Fields Too Large
451 	Unavailable For Legal Reasons
  	 
5xx Server Error 	 
500 	Internal Server Error
501 	Not Implemented
502 	Bad Gateway
503 	Service Unavailable
504 	Gateway Timeout
505 	HTTP Version Not Supported
506 	Variant Also Negotiates
507 	Insufficient Storage
508 	Loop Detected
510 	Not Extended
511 	Network Authentication Required

---
- Cómo ver todos tus puertos abiertos:
```
netstat -putona
netstat -nlptn
```

---
¿Cómo instalar tool **Volatility**?
https://behacker.pro/que-es-volatility-y-como-instalarloinstalacion-no-standalone-en-windows-10/

![[volatility_commands.png]]

---