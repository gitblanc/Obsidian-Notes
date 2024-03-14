# The Extensions Interface
Let's start by taking a look through the Extensions interface:

![](img/Pasted%20image%2020230828134020.png)

The default view in the Extensions interface gives us an overview of the extensions that we have loaded into Burp Suite. There are none in the screenshot above -- we will change this in the next few tasks. The first box (towards the top of the interface) provides us with a list of extensions that we have installed and allows us to activate or deactivate them for this project.

The options to the left of this box allow us to uninstall extensions with the Remove button or install new ones from files on our disk with the Add button. These could be either modules that we have coded or modules that have been made available on the internet but are not in the BApp store. The Up and Down buttons in this section control the order that installed extensions are listed in. Extensions are invoked in _descending_ order based on this list. In other words: all traffic passing through Burp Suite will be passed through each extension in order, starting at the top of the list and working down. This can be very important when dealing with extensions that modify the requests as some may counteract or otherwise hinder one another.  

Towards the bottom of the window, we have Details, Output and Errors for the currently selected module. These can be used to view module information, as well as for debugging.

# The BApp store

The Burp App Store (or BApp Store for short) gives us a way to easily list official extensions and integrate them seamlessly with Burp Suite. Extensions can be written in a variety of languages -- most commonly Java (which integrates into the framework automatically) or Python (which requires the Jython interpreter -- more on this in the next task!).  
  
Let's start by installing a Java extension, just to get a feel for the BApp store.  
  
The [Request Timer](https://github.com/portswigger/request-timer) extension (Written by Nick Taylor) allows us to log the time that each request we send takes to receive a response; this can be extremely useful for discovering the presence of (and exploiting) time-based vulnerabilities. For example, if a login form takes an extra second to process requests that contain a valid username than it does for accounts that do not exist, then we can quickly generate a list of possible usernames and use the difference in times to see which usernames are valid.

Switch over to the "BApp Store" sub-tab, then search for "Request Timer". There should only be one result. Click on the returned Extension, then click "Install":

![video demo](https://tryhackme-images.s3.amazonaws.com/user-uploads/5d9e176315f8850e719252ed/room-content/7a9077f19a68a81647874639a6afaeb4.gif)

Notice that a new tab appeared in the main menu at the top of the screen. Different extensions have different behaviours: some merely add a new item to right-click context menus; others create entirely new tabs in the main menu bar.

As this was just an example of using the BApp store, we won't cover using the Request Timer here; however, switching to the new tab and taking a look is highly recommended!

# Jython

If we want to use Python modules in Burp Suite, we need to have downloaded and included the separate Jython Interpreter JAR file. The Jython interpreter is a Java implementation of Python. The website gives us the option to either install Jython to our system or download it as a standalone Java archive (JAR). We need it as a standalone archive to integrate it with Burp.  

_**Note:** we can do the same thing with Ruby modules and the JRuby integration; however, we will not cover this here as: A) Python modules are much more common and B) it's exactly the same process for both._

First up, we need to download an up-to-date copy of the Jython JAR archive from the [Jython website](https://www.jython.org/download). We are looking for the **_Jython Standalone_** option:

![](img/Pasted%20image%2020230828134545.png)

Save the JAR file somewhere on your disk, then switch to the "Options" sub-tab in Extender.

Scroll down to the "Python Environment" section, and set the "Location of Jython standalone JAR file" to the path of the archive:

![](img/Pasted%20image%2020230828134604.png)

Simple as that, we can now install Python modules from the BApp store!  

This is a very simple step that significantly increases the number of extensions available to us.  

_**Note:** Due to the multi-platform nature of Java, the exact same steps will work for adding Jython to Burp Suite on any operating system._

# The Burp Suite API

Whilst coding our own modules is far outwith the scope of this module, it is worth looking (very briefly) at how such a task might be approached.

Extender exposes a large number of API Endpoints that new modules can hook into when integrating with Burp Suite.  

We can view these in the "APIs" sub-tab:

![](img/Pasted%20image%2020230828134850.png)

Each item in the list on the left of this sub-tab documents a different API endpoint -- all of which can be called from within extensions. The endpoints here give developers a lot of power when writing extensions to interact seamlessly with the existing functionality of Burp Suite. As you may expect, we can interact with these endpoints in any of the languages supported by Burp Suite for use in extensions: Java (natively), Python (via Jython), and Ruby (via JRuby).  

If you are particularly interested in coding your own extensions for Burp Suite, PortSwigger provide a wonderful reference which can be found [here](https://portswigger.net/burp/extender/writing-your-first-burp-suite-extension).
