Note: open as **root**
````
cd /etc/ssh

mkdir keys_backup_ssh #create backup folder

mv ssh_host_* keys_backup_ssh #move the SSH keys to the backup folder

dpkg-reconfigure openssh-server #generate new keyset

service ssh start #start SSH from command line

netstat -antp #verify that the service is running

service ssh stop #stop SSH
````