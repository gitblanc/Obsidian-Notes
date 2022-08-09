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