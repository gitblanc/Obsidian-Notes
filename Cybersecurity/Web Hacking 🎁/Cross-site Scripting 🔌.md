- **Cross-site Scripting (XSS)** -> injection attack where malicious JavaScript gets injected into a web application with the intention of being executed by other users.
- **Payload** -> JavaScript code we wish to be executed on the targets computer. It has two parts, the *intention* and the *modification*.
	- **Intention** -> what you wish the JavaScript to actually do.
	- **Modification** -> changes to the code we need to make it execute as every scenario is different.
- Proof of content, session stealing, key logger, business logic.
- **Reflected XSS** -> happens when user-supplied data in an HTTP request is included in the webpage source without any validation.
- **Stored XSS** -> this payload is stored on the web application and then gets run when other users visit the site or the web page.
- **DOM Based XSS** -> DOM stands for Document Object Model and is a programming interface for HTML and XML documents. More about DOM on https://w3.org/TR/REC-DOM-Level-1/Introduction.html. DOM Based XSS is where the JavaScript execution happens directly in the browser without any new pages being loaded or data submitted to backend code. Method eval().
- **Blind XSS** -> the payload gets stored on the website for another user to view, but you can't see the payload working or be able to test it against yourself first. Popular tool for this attack is xsshunter: https://xsshunter.com
- **onload event** -> executes the code of your choosing once the image specified is the src attribute has loaded onto the webpage.
- **Polyglots** -> is a string of text which can escape attributes, tags, bypass filters all in one.

![[xss1.png]]
![[xss2.png]]
![[xss3.png]]
![[xss4.png]]
![[xss5.png]]
![[xss6.png]]
![[xss7.png]]
![[xss8.png]]
![[xss9.png]]
![[xss10.png]]
![[xss11.png]]
![[xss12.png]]
![[xss13.png]]
![[xss14.png]]
![[xss15.png]]
![[xss16.png]]
![[xss17.png]]
![[xss18.png]]
![[xss19.png]]
![[xss20.png]]
![[xss21.png]]
![[xss22.png]]