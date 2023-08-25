# What is Burp Suite?
Put simply: Burp Suite is a framework written in Java that aims to provide a one-stop-shop for web application penetration testing. In many ways, this goal is achieved as Burp is very much the industry standard tool for hands-on web app security assessments. Burp Suite is also very commonly used when assessing mobile applications, as the same features which make it so attractive for web app testing translate almost perfectly into testing the APIs (**A**pplication **P**rogramming **I**nterfaces) powering most mobile apps.  

At the simplest level, Burp can capture and manipulate all of the traffic between an attacker and a webserver: this is the core of the framework. After capturing requests, we can choose to send them to various other parts of the Burp Suite framework -- we will be covering some of these tools in upcoming rooms. This ability to intercept, view, and modify web requests prior to them being sent to the target server (or, in some cases, the responses before they are received by our browser), makes Burp Suite perfect for any kind of manual web app testing.  

There are various different editions of Burp Suite available. We will be working with the **Burp Suite Community** edition, as this is free to use for any (legal) non-commercial use. The Burp Suite _Professional_ and _Enterprise_ editions both require expensive licenses but come with powerful extra features:

- **Burp Suite Professional** is an unrestricted version of Burp Suite Community. It comes with features such as:
    - An automated vulnerability scanner
    - A fuzzer/bruteforcer that isn't rate limited
    - Saving projects for future use; report generation
    - A built-in API to allow integration with other tools
    - Unrestricted access to add new extensions for greater functionality
    - Access to the Burp Suite Collaborator (effectively providing a unique request catcher self-hosted or running on a Portswigger owned server)
    In short, Burp Pro is an _extremely_ powerful tool -- which is why it comes with a £319/$399 price tag per user for a one-year subscription. For this reason, Burp Pro is usually only used by professionals (with licenses often being provided by employers).
- **Burp Suite Enterprise** is slightly different. Unlike the community and professional editions, Burp Enterprise is used for continuous scanning. It provides an automated scanner that can periodically scan webapps for vulnerabilities in much the same way as software like [Nessus](https://tryhackme.com/room/rpnessusredux) performs  automated infrastructure scanning. Unlike the other editions of Burp Suite which allow you to perform manual attacks from your own computer, Enterprise sits on a server and constantly scans target web apps for vulnerabilities.  
    
Due to the prohibitive costs involved with either of these editions of Burp Suite, we will stick to the core feature-set provided by Burp Suite Community.

_**Note:** Burp Suite for Windows is featured in the screenshots for many demonstrations; however, there are no differences between this and the copy of Burp Suite installed on the AttackBox._

# Features of Burp Community

Whilst Burp Community has a relatively limited feature-set compared to the Professional edition, it still has many superb tools available. These include:  

- **Proxy:** The most well-known aspect of Burp Suite, the Burp Proxy allows us to intercept and modify requests/responses when interacting with web applications.
- **Repeater:** The second most well-known Burp feature -- [Repeater](https://tryhackme.com/room/burpsuiterepeater) -- allows us to capture, modify, then resend the same request numerous times. This feature can be absolutely invaluable, especially when we need to craft a payload through trial and error (e.g. in an SQLi -- **S**tructured **Q**uery **L**anguage **I**njection) or when testing the functionality of an endpoint for flaws.
- **Intruder:** Although harshly rate-limited in Burp Community, [Intruder](https://tryhackme.com/room/burpsuiteintruder) allows us to spray an endpoint with requests. This is often used for bruteforce attacks or to fuzz endpoints.
- **Decoder:** Though less-used than the previously mentioned features, [Decoder](https://tryhackme.com/room/burpsuiteom) still provides a valuable service when transforming data -- either in terms of decoding captured information, or encoding a payload prior to sending it to the target. Whilst there are other services available to do the same job, doing this directly within Burp Suite can be very efficient.  
- **Comparer:** As the name suggests, [Comparer](https://tryhackme.com/room/burpsuiteom) allows us to compare two pieces of data at either word or byte level. Again, this is not something that is unique to Burp Suite, but being able to send (potentially very large) pieces of data directly into a comparison tool with a single keyboard shortcut can speed things up considerably.  
- **Sequencer:** We usually use [Sequencer](https://tryhackme.com/room/burpsuiteom) when assessing the randomness of tokens such as session cookie values or other supposedly random generated data. If the algorithm is not generating secure random values, then this could open up some devastating avenues for attack.  

In addition to the myriad of in-built features, the Java codebase also makes it very easy to write extensions to add to the functionality of the Burp framework. These can be written in Java, Python (using the Java [Jython](https://www.jython.org/) interpreter), or Ruby (using the Java [JRuby](https://www.jruby.org/) interpreter). The Burp Suite [Extender](https://tryhackme.com/room/burpsuiteextender) module can quickly and easily load extensions into the framework, as well as providing a marketplace to download third-party modules (referred to as the "BApp Store"). Whilst many of these extensions require a professional license to download and add in, there are still a fair number that can be integrated with Burp Community. For example, we may wish to extend the inbuilt logging functionality of Burp Suite with the [Logger++](https://github.com/portswigger/logger-plus-plus) module.

# Dashboard
When we open Burp Suite and have accepted the terms and conditions, we are met with a window asking us to select the project type.  

This window doesn't give us many options in Burp Community. Burp Pro would allow us to save our work to the disk or load a previously saved project at this point. All we can do here is click "Next", however.

The next window allows us to choose a configuration for Burp Suite. Leaving this at the default is perfect for most situations:  

Click "Start Burp", and the main Burp Suite interface will open!

---

The first time you open Burp Suite, you may be presented with a screen of training options. These are well worth reading through if you get the time.  

If not (and in any subsequent sessions regardless), you will be presented with the slightly daunting Burp Dashboard:

![](./img/Pasted%20image%2020230825104239.png)

Don't be alarmed if this doesn't make too much sense just yet -- it soon will!

In short, the Dashboard interface is split into four quadrants:

![](./img/Pasted%20image%2020230825104318.png)

- The Tasks menu allows us to define background tasks that Burp Suite will run whilst we use the application. The Pro version would also allow us to create on-demand scans. The default "Live Passive Crawl" (which automatically logs the pages we visit) will be more than suitable for our uses in this module.
- The Event log tells us what Burp Suite is doing (e.g. starting the Proxy), as well as information about any connections that we are making through Burp.
- The Issue Activity section is exclusive to Burp Pro. It won't give us anything using Burp Community, but in Burp Professional it would list all of the vulnerabilities found by the automated scanner. These would be ranked by severity and filterable by how sure Burp is that the component is vulnerable.
- The Advisory section gives more information about the vulnerabilities found, as well as references and suggested remediations. These could then be exported into a report.  
    Clicking on one of the example vulnerabilities in the Issue Activity section gives us an idea of what this looks like:

![](./img/Pasted%20image%2020230825104343.png)

Throughout the various tabs and windows of Burp Suite, you will find little help icons: a question mark within a circle.

Clicking on these will open a new window containing help for the section, for example:

![](./img/Pasted%20image%2020230825104415.png)

These are extremely useful if you're ever stuck and don't know what a feature does, so make good use of them!

# Navigation
Navigating around the Burp Suite GUI by default is done entirely using the top menu bars:

![](./img/Pasted%20image%2020230825104650.png)

These allow you to switch between modules (along the top row of the attached image). If the selected module has more than one sub-tab, then these can be selected using a second menu bar which appears directly below the original bar (the bottom row of the image above). It is common for module-specific settings to be provided in these sub-tabs (as is the case with the Proxy Options above).  

Tabs can also be popped out into separate windows should you prefer to view multiple tabs separately. This can be done by clicking "Window" in the application menu at the top of the screen, then choosing to "Detach" tabs:

![](./img/Pasted%20image%2020230825104707.png)

These can be reattached in the same way.  

In addition to the menu bar, Burp Suite also has keyboard shortcuts that allow quick navigation to key tabs. By default, these are:

|**Shortcut**|**Does**|
|---|---|
|`Ctrl + Shift + D`|Switch to the Dashboard|
|`Ctrl + Shift + T`|Switch to the Target tab|
|`Ctrl + Shift + P   `|Switch to the Proxy tab|
|`Ctrl + Shift + I   `|Switch to the Intruder tab|
|`Ctrl + Shift + R   `|Switch to the Repeater tab|

We will look at how we can view and change these in the next task.

# Options
Before we start learning about the Burp Proxy, let's take a look at the options available for configuring Burp Suite.

There are two types of settings: Global Settings (also called User Settings), and Project Settings.  

User settings affect the Burp Suite installation as a whole and will be applied every time we start the application. By contrast, Project Settings only apply to the current project. Given that we can't save projects in Burp Suite Community Edition, this effectively means that any project options we set will be lost every time we close Burp.

Many options are provided as both global settings (which are used to set a baseline) and project settings (which can be used to override the equivalent global setting).

**_Note:_** _The settings system in Burp Suite was recently completely revamped. This task has been updated to use the new version. Please ensure that you are using the latest version of Burp Suite._  

---

The Settings window can be accessed by clicking on the "Settings" button in the top navigation bar:

![](./img/Pasted%20image%2020230825104912.png)

Clicking this button opens a separate settings window, as shown below:

![](./img/Pasted%20image%2020230825104927.png)

On the left hand side we have a menu containing options to change the scope between all settings, user settings, and project settings, as well as search for specific settings, or select them by category.  

It should be noted that many of the tools in Burp Suite offer shortcuts to specific categories of settings. For example, the Proxy tool includes a "Proxy settings" button which will open the Settings window directly to the section relevant to the proxy.

![](./img/Pasted%20image%2020230825104945.png)

The Search feature of the settings page is a relatively new addition; however, it is absolutely invaluable, allowing us to search for settings using keywords.

Familiarise yourself with the range of configurable options in Burp Suite, then complete the following exercises.

To change to dark mode -> Settings > User > Display

# Introduction to the Burp Proxy
The Burp Proxy is the most fundamental (and most important!) of the tools available in Burp Suite. It allows us to capture requests and responses between ourselves and our target. These can then be manipulated or sent to other tools for further processing before being allowed to continue to their destination.

For example, if we make a request to `https://tryhackme.com` through the Burp Proxy, our request will be captured and won't be allowed to continue to the TryHackMe servers until we explicitly allow it through. We can choose to do the same with the response from the server, although this isn't active by default. This ability to intercept requests ultimately means that we can take complete control over our web traffic -- an invaluable ability when it comes to testing web applications.

---

There are a few configurations we need to make before we can use the proxy, but let's start by looking at the interface.

_**Note:** You do not need to follow along with this task -- just read the information and understand what the Proxy is used for._  

When we first open the Proxy tab, Burp gives us a bunch of useful information and background reading. This information is well worth reading through; however, the real magic happens after we capture a request:
![](./img/Pasted%20image%2020230825105714.png)

With the proxy active, a request was made to the TryHackMe website. At this point, the browser making the request will hang, and the request will appear in the Proxy tab giving us the view shown in the screenshot above. We can then choose to forward or drop the request (potentially after editing it). We can also do various other things here, such as sending the request to one of the other Burp modules, copying it as a cURL command, saving it to a file, and many others.

When we have finished working with the Proxy, we can click the "Intercept is on" button to disable the Intercept, which will allow requests to pass through the proxy without being stopped.

---

Burp Suite will still (by default) be logging requests made through the proxy when the intercept is off. This can be very useful for going back and analysing prior requests, even if we didn't specifically capture them when they were made.

Burp will also capture and log WebSocket communication, which, again, can be exceedingly helpful when analysing a web app.

The logs can be viewed by going to the "HTTP history" and "WebSockets history" sub-tabs:

![](./img/Pasted%20image%2020230825105739.png)

It is worth noting that any requests captured here can be sent to other tools in the framework by right-clicking them and choosing "Send to...". For example, we could take a previous HTTP request that has already been proxied to the target and send it to [Repeater](https://tryhackme.com/room/burpsuiterepeater).  

---

Finally, there are also Proxy specific options, which in the Proxy Settings, accessible by clicking on the "Proxy Settings" button.

These options give us a _lot_ of control over how the proxy operates, so it is an excellent idea to familiarise yourself with these.  

For example, the proxy will not intercept server responses by default unless we explicitly ask it to on a per-request basis. We can override the default setting by selecting the "Intercept responses based on the following rules" checkbox and picking one or more rules. The "`Or` `Request` `Was Intercepted`" rule is good for catching responses to all requests that were intercepted by the proxy:

![](./img/Pasted%20image%2020230825105759.png)

The "`And` `URL` `Is in target scope`" is another very good default rule; we will look at scoping later in this room.  

You can make your own rules for most of the Proxy options, so this is one section where looking around and experimenting will serve you very well indeed!

Another particularly useful section of this sub-tab is the "Match and Replace" section; this allows you to perform regexes on incoming and outgoing requests. For example, you can automatically change your user agent to emulate a different web browser in outgoing requests or remove all cookies being set in incoming requests. Again, you are free to make your own rules here.

# Connecting through the Proxy (FoxyProxy)
You've seen the theory; now it's time to start using the proxy for yourself.

There are two ways to proxy our traffic through Burp Suite.

1. We could use the embedded browser (**we will cover this in a later task**).
2. We can configure our local web browser to proxy our traffic through Burp; this is more common and so will be the focus of this task.

---

The Burp Proxy works by opening a web interface on `127.0.0.1:8080` (by default). As implied by the fact that this is a "proxy", we need to redirect all of our browser traffic through this port before we can start intercepting it with Burp. We can do this by altering our browser settings or, more commonly, by using a Firefox browser extension called [FoxyProxy](https://getfoxyproxy.org/). FoxyProxy allows us to save proxy profiles, meaning we can quickly and easily switch to our "Burp Suite" profile in a matter of clicks, then disable the proxy just as easily.

_**Note:** All instructions will be given with Firefox in mind, as this is the default browser for both Kali Linux and the TryHackMe AttackBox. If you are using another browser locally then you are advised to use the AttackBox, or you may otherwise need to find alternative methods to those presented in this task. If you can't get the proxy working in your local browser and do not want to use the AttackBox, then you may wish to skip ahead to the Burp Suite Browser task._

---

There are two versions of FoxyProxy: _Basic_ and _Standard_. Both versions allow you to change your proxy settings on the fly; however, FoxyProxy Standard gives you a lot more control over what traffic gets sent through the proxy. For example, it will allow you to set pattern matching rules to determine whether a request should be proxied or not: this is more complicated than the simple proxy offered by FoxyProxy basic.  

The basic edition is more than adequate for our usage. It is pre-installed and configured in the Firefox browser of the AttackBox, so if you are using the AttackBox, please feel free to skip ahead to the last section of this task.

If you are using your own machine, you can download FoxyProxy Basic [here](https://addons.mozilla.org/en-US/firefox/addon/foxyproxy-basic/).

Once installed, a button should appear at the top right of the screen which allows you to access your proxy configurations:

![](./img/Pasted%20image%2020230825110234.png)

There are no default configurations, so let's click on the "Options" button to create our Burp Proxy config.

This will open a new browser tab with the FoxyProxy options page:

![](./img/Pasted%20image%2020230825110252.png)

Click on the "Add" button and fill in the following values:
- Title: `Burp` (or anything else you prefer)
- Proxy IP: `127.0.0.1`
- Port: `8080`

![](./img/Pasted%20image%2020230825110313.png)

Now click "Save".

---

When you click on the FoxyProxy icon at the top of the screen, you will see that that there is a configuration available for Burp:

![](./img/Pasted%20image%2020230825110329.png)

If we click on the "Burp" config, our browser will start directing all of our traffic through `127.0.0.1:8080`. **Be warned**: if Burp Suite is not running, your browser will not be able to make any requests when this config is activated!  

Activate this config now -- the icon in the menu should change to indicate that we have a proxy running:

![](./img/Pasted%20image%2020230825110348.png)

Next, switch over to Burp Suite and make sure the Intercept is On:

![](./img/Pasted%20image%2020230825110418.png)

Now, try accessing the homepage for `http://10.10.81.3/` in Firefox. Your browser should hang, and your proxy will populate with the request headers.

Congratulations, you just intercepted your first request!

From here, you can choose to forward or drop the request. Alternatively, you could send it to another tool or perform any number of other actions by right-clicking on the request and selecting an option from the right-click menu.

_**Remember:**_ _Whilst you are connected to the proxy and have the Proxy Intercept switched on, your browser will hang whenever you make a request. A very common mistake when you are learning to use Burp Suite (and indeed, later on!) is to accidentally leave the intercept switched on and ergo be unable to make any web requests through your browser. If your browser is hanging and you don't know why: check your proxy!_

# Proxying HTTPS
Great, so we can intercept HTTP traffic -- what's next?

Unfortunately, there's a problem. What happens if we navigate to a site with TLS enabled? For example, `https://google.com/`:

![](./img/Pasted%20image%2020230825110737.png)

We get an error.

Specifically, Firefox is telling us that the Portswigger **C**ertificate **A**uthority (CA) isn't authorised to secure the connection.

Fortunately, Burp offers us an easy way around this. We need to get Firefox to trust connections secured by Portswigger certs, so we will manually add the CA certificate to our list of trusted certificate authorities.

First, with the proxy activated head to [http://burp/cert](http://burp/cert); this will download a file called `cacert.der` -- save it somewhere on your machine.

Next, type `about:preferences` into your Firefox search bar and press enter; this takes us to the FireFox settings page. Search the page for "certificates" and we find the option to "View Certificates":

![](./img/Pasted%20image%2020230825110804.png)

Clicking the "View Certificates" button allows us to see all of our trusted CA certificates. We can register a new certificate for Portswigger by pressing "Import" and selecting the file that we just downloaded.

In the menu that pops up, select "Trust this CA to identify websites", then click Ok:

![](./img/Pasted%20image%2020230825110825.png)

We should now be free to visit any TLS enabled sites that we wish!

The following video shows the full import process:

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5d9e176315f8850e719252ed/room-content/fb2a8717ae887eda024a7791d83cefaf.gif)

# The Burp Suite Browser
If the last few tasks seemed overly complex, rest assured, this topic will be a lot simpler.

In addition to giving us the option to modify our regular web browser to work with the proxy, Burp Suite also includes a built-in Chromium browser that is pre-configured to use the proxy without any of the modifications we just had to do.  

Whilst this may seem ideal, it is not as commonly used as the process detailed in the previous few tasks. People tend to stick with their own browser as it gives them a lot more customisability; however, both are perfectly valid choices.

We can start the Burp Browser with the "Open Browser" button in the proxy tab:

![](./img/Pasted%20image%2020230825111318.png)

A Chromium window will now pop up. Any requests we make in this will go through the proxy.

_**Note:** There are many settings to do with the Burp Browser in the Project options and User options tabs -- make sure to go look at them!_

---

If we are running on Linux as the root user (as we are with the AttackBox), Burp Suite is unable to create a sandbox environment to start the Burp Browser in, causing it to throw an error and die:

![](./img/Pasted%20image%2020230825111348.png)

There are two simple solutions to this:
- **The smart option:** We could create a new user and run Burp Suite under a low privilege account.
- **The easy option:** We could go to `Project options -> Misc -> Embedded Browser` and check the  `Allow the embedded browser to run without a sandbox` option. Checking this option will allow the browser to start, but be aware that it is disabled by default for security reasons: if we get compromised using the browser, then an attacker will have access to our entire machine. On the training environment of the AttackBox this is unlikely (and isn't a huge issue even if it _does_ happen), but keep it in mind if you try this on a local installation of Burp Suite.

Be aware that you will need to do this if using the embedded browser on the AttackBox.

# Scoping and Targeting

Finally, we come to one of the most important parts of using the Burp Proxy: Scoping.

It can get extremely tedious having Burp capturing all of our traffic. When it logs everything (including traffic to sites we aren't targeting), it muddies up logs we may later wish to send to clients. In short, allowing Burp to capture _everything_ can quickly become a massive pain.

What's the solution? Scoping.

Setting a scope for the project allows us to define what gets proxied and logged. We can restrict Burp Suite to _only_ target the web application(s) that we want to test. The easiest way to do this is by switching over to the "Target" tab, right-clicking our target from our list on the left, then choosing "Add To Scope". Burp will then ask us whether we want to stop logging anything which isn't in scope -- most of the time we want to choose "yes" here.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5d9e176315f8850e719252ed/room-content/7e11c5dec4dba4336927aa7561e5c793.gif)

We can now check our scope by switching to the "Scope" sub-tab (as shown in the GIF above).

The Scope Settings window allows us to control what we are targeting by either _Including_ or _Excluding_ domains / IPs. This is a very powerful section, so it's well worth taking the time to get accustomed to using it.  

---

We just chose to disable _logging_ for out of scope traffic, but the proxy will still be intercepting everything. To turn this off, we need to go into the Proxy Options sub-tab and select "`And` `URL` `Is in target scope`" from the Intercept Client Requests section:

![](./img/Pasted%20image%2020230825111555.png)

With this option selected, the proxy will completely ignore anything that isn't in the scope, vastly cleaning up the traffic coming through Burp.

# Site Map and Issue Definitions
Control of the scope may be the most useful aspect of the Target tab, but it's by no means the _only_ use for this section of Burp.

There are three sub-tabs under _Target_:
- **Site map** allows us to map out the apps we are targeting in a tree structure. Every page that we visit will show up here, allowing us to automatically generate a site map for the target simply by browsing around the web app. Burp Pro would also allow us to spider the targets automatically (i.e. look through every page for links and use them to map out as much of the site as-is publicly accessible using the links between pages); however, with Burp Community, we can still use this to accumulate data whilst we perform our initial enumeration steps.  
    The Site map can be especially useful if we want to map out an API, as whenever we visit a page, any API endpoints that the page retrieves data from whilst loading will show up here.
- **Scope Settings:** We have already seen the Scope Settings window — it allows us to control Burp's target scope for the project.
- **Issue Definitions:** Whilst we don't have access to the Burp Suite vulnerability scanner in Burp Community, we do still have access to a list of all the vulnerabilities it looks for. The Issue Definitions section gives us a huge list of web vulnerabilities (complete with descriptions and references) which we can draw from should we need citations for a report or help describing a vulnerability.
