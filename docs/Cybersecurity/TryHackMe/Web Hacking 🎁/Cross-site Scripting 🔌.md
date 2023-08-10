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

![](./img/xss1.png)
![](./img/xss2.png)
![](./img/xss3.png)
![](./img/xss4.png)
![](./img/xss5.png)
![](./img/xss6.png)
![](./img/xss7.png)
![](./img/xss8.png)
![](./img/xss9.png)
![](./img/xss10.png)
![](./img/xss11.png)
![](./img/xss12.png)
![](./img/xss13.png)
![](./img/xss14.png)
![](./img/xss15.png)
![](./img/xss16.png)
![](./img/xss17.png)
![](./img/xss18.png)
![](./img/xss19.png)
![](./img/xss20.png)
![](./img/xss21.png)
![](./img/xss22.png)