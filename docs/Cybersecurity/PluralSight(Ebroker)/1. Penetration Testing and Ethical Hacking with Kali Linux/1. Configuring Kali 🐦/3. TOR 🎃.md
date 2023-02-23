![[tor.png]]

Note: open as **root**
````
apt-get install tor #install tor

leafpad /etc/proxychains4.conf #edit proxy configuration
````

![[proxychain.png]]

![[proxychain2.png]]

````
service tor start 

service tor status #verify that tor is working

firefox www.whatismyip.com #open a webpage

proxychains firefox www.whatismyip.com #open a webpage with tor routing
````