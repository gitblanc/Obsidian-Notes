- **OSINT** -> Open-Source Intelligence.
- **Robots.txt** -> file that tells search engines which pages they are and aren't allowed to show.
- **Favicon** -> is a small icon displayed in the browser's address bar or tab used for branding a website.
- **Sitemap.xml** -> gives a list of every file the website owner wishes to be listed on a search engine. Can list difficult areas to access or even some old webpages that the current site no longer uses.
- **HTTP Headers** -> headers that can contain useful information such as the webserver software and the scripting language in use. You can use `curl <ipaddr> <options>`.
- **Google hacking/Dorking** -> uses advanced search engine features, which allows us to pick out custom content. More information on https://en.wikipedia.org/wiki/Google_hacking
- **Wappalyzer** 
- **Wayback Machine** -> is an historical archive of websites that dates back to the late 90s. Search https://archive.org/web/.
- **S3 Buckets** -> are a storage service provided by Amazon AWS, allowing people to save files and even static website content in the cloud accesible over HTTP and HTTPS.
- **Automated Discovery** -> process of using tools to discover content rather than doing it manually.
- **WordLists** -> text files that contain a long list of commonly used words. You can use:
	- `ffuf -w <wordlist> -u <ipaddr/FUZZ>`
	- `dirb <ipaddr> <wordlist
	- `gobuster dir --url <ipaddr> -w <wordlist>`

![[robots.png]]
![[favicon 1.png]]
![[favicon 2.png]]
![[sitemap.png]]
![[headers.png]]
![[framework stack.png]]
![[google dorking.png]]
![[s3 amazon.png]]
![[automated 1.png]]
![[automated 2.png]]