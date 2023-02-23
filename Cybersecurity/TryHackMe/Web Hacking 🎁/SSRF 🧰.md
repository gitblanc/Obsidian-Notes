- **SSRF** -> means Server-Side Request Forgery. Vulnerability that allows a malicious user to cause the webserver to make an aditional or edited HTTP request to the resource of the attacker's choosing.
- 2 types:
	- **Regular** -> data is returned to the attacker's screen.
	- **Blind** -> no information is returned to the attacker's screen.
- Impact:
	- Access to unauthorised areas
	- Access to customer/organisational data
	- Ability to Scale to internal networks
	- Reveal authentication tokens/credentials
- Ways to spot a SSRF:
	- When a full URL is used in a parameter in the address bar
	- Partial url such as just the hostname or the path of the url
	- Hidden in a form
- If working with a blind SSRF where no output is reflected back to us, we can use an external HTTP logging tool to monitor requests such as `requestbin.com` or Burp Suite.
- **Deny List** -> it is used to stop certain input
- **Allow List** -> it is used to permit only certain inputs
- **Open Redirect** -> allows to bypass strict rules

![[ssrf1.png]]
![[ssrf2.png]]
![[ssrf3.png]]
![[ssrf4.png]]
![[ssrf5.png]]
![[ssrf6.png]]
![[ssrf7.png]]
![[ssrf8.png]]
![[ssrf9.png]]