# What is Intruder?
Intruder is Burp Suite's in-built fuzzing tool. It allows us to take a request (usually captured in the Proxy before being passed into Intruder) and use it as a template to send many more requests with slightly altered values automatically. For example, by capturing a request containing a login attempt, we could then configure Intruder to swap out the username and password fields for values from a wordlist, effectively allowing us to bruteforce the login form. Similarly, we could pass in a fuzzing[1] wordlist and use Intruder to fuzz for subdirectories, endpoints, or virtual hosts. This functionality is very similar to that provided by command-line tools such as Wfuzz or Ffuf.  

In short, as a method for automating requests, Intruder is extremely powerful -- there is just one problem: to access the full speed of Intruder, we need Burp Professional. We _can_ still use Intruder with Burp Community, but it is heavily rate-limited. This speed restriction means that many hackers choose to use other tools for fuzzing and bruteforcing.

Limitations aside, Intruder is still very useful, so it is well worth learning to use it properly.

---

Let's take a look at the Intruder interface:

![](img/Pasted%20image%2020230827210423.png)

The first view we get is a relatively sparse interface that allows us to choose our target. Assuming that we sent a request in from the Proxy (by using `Ctrl + I` or right-clicking and selecting "Send to Intruder"), this should already be populated for us.

There are four other Intruder sub-tabs:
- **Positions** allows us to select an Attack Type (we will cover these in an upcoming task), as well as configure where in the request template we wish to insert our payloads.  
- **Payloads** allows us to select values to insert into each of the positions we defined in the previous sub-tab. For example, we may choose to load items in from a wordlist to serve as payloads. How these get inserted into the template depends on the attack type we chose in the Positions tab. There are many payload types to choose from (anything from a simple wordlist to regexes based on responses from the server). The Payloads sub-tab also allows us to alter Intruder's behaviour with regards to payloads; for example, we can define pre-processing rules to apply to each payload (e.g. add a prefix or suffix, match and replace, or skip if the payload matches a defined regex).  
- **Resource Pool** is not particularly useful to us in Burp Community. It allows us to divide our resources between tasks. Burp Pro would allow us to run various types of automated tasks in the background, which is where we may wish to manually allocate our available memory and processing power between these automated tasks and Intruder. Without access to these automated tasks, there is little point in using this, so we won't devote much time to it.
- As with most of the other Burp tools, Intruder allows us to configure attack behaviour in the **Options** sub-tab. The settings here apply primarily to how Burp handles results and how Burp handles the attack itself. For example, we can choose to flag requests that contain specified pieces of text or define how Burp responds to redirect (3xx) responses.

We will take a closer look at some of these sub-tabs in the upcoming tasks. For now, just get to know where things are in the interface.

---

1. Fuzzing is when we take a set of data and apply it to a parameter to test functionality or to see if something exists. For example, we may choose to "fuzz for endpoints" in a web application; this would involve taking each word in a wordlist and adding it to the end of a request to see how the web server responds (e.g. `http://10.10.88.90/WORD_GOES_HERE`).  

---

# Positions
When we are looking to perform an attack with Intruder, the first thing we need to do is look at _positions._ Positions tell Intruder where to insert payloads (which we will look at in upcoming tasks).  
Let's switch over to the Positions sub-tab:

![](img/Pasted%20image%2020230828110250.png)

Notice that Burp will attempt to determine the most likely places we may wish to insert a payload automatically -- these are highlighted in green and surrounded by silcrows (`§`).

On the right-hand side of the interface, we have the buttons labelled "Add §", "Clear §", and "Auto §":
- **Add** lets us define new positions by highlighting them in the editor and clicking the button.
- **Clear** removes all defined positions, leaving us with a blank canvas to define our own.
- **Auto** attempts to select the most likely positions automatically; this is useful if we cleared the default positions and want them back.

Here is a GIF demonstrating the process of adding, clearing, and automatically reselecting positions:

![video demo](https://tryhackme-images.s3.amazonaws.com/user-uploads/5d9e176315f8850e719252ed/room-content/35caa3d4e70aae2084966b1928c3db5f.gif)

Select the value of the "Host" header and add it as a position.
Your editor should look something like this:

![](img/Pasted%20image%2020230828110348.png)

# Introduction

Let's switch to the "Positions" sub-tab and look in the "Attack types" drop-down menu.
There are four attack types available:
- Sniper
- Battering ram
- Pitchfork
- Cluster bomb
We will look at each of these in turn.

# Sniper

Sniper is the first and most common attack type.

When conducting a sniper attack, we provide _one_ set of payloads. For example, this could be a single file containing a wordlist or a range of numbers. From here on out, we will refer to a list of items to be slotted into requests using the Burp Suite terminology of a "Payload Set". Intruder will take each payload in a payload set and put it into each defined position in turn.

Take a look at our example template from before:
```html
POST /support/login/ HTTP/1.1
Host: 10.10.52.70
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:80.0) Gecko/20100101 Firefox/80.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 37
Origin: http://10.10.52.70
Connection: close
Referer: http://10.10.52.70/support/login/
Upgrade-Insecure-Requests: 1

username=§pentester§&password=§Expl01ted§
```

There are two positions defined here, targeting the `username` and `password` body parameters.
In a sniper attack, Intruder will take each position and substitute each payload into it in turn.
For example, let's assume we have a wordlist with three words in it: `burp`, `suite`, and `intruder`.
With the two positions that we have above, Intruder would use these words to make **_six_** requests:

|**Request Number**|**Request Body**|
|---|---|
|1|`username=burp&password=Expl01ted`|
|2|`username=suite&password=Expl01ted`|
|3|`username=intruder&password=Expl01ted`|
|4|`username=pentester&password=burp`|
|5|`username=pentester&password=suite`|
|6|`username=pentester&password=intruder`|

Notice how Intruder starts with the first position (`username`) and tries each of our payloads, then moves to the second position and tries the same payloads again. We can calculate the number of requests that Intruder Sniper will make as `requests = numberOfWords * numberOfPositions`.  

This quality makes Sniper very good for single-position attacks (e.g. a password bruteforce if we know the username or _fuzzing for API endpoint_s).

# Battering Ram
Next, let's take a look at the _Battering Ram_ Attack type.

Like Sniper, Battering ram takes _one_ set of payloads (e.g. one wordlist). _Un_like Sniper, the Battering ram puts the same payload in _every_ position rather than in each position in turn.  

Let's use the same wordlist and example request as we did in the last task to illustrate this.

```html
POST /support/login/ HTTP/1.1
Host: 10.10.52.70
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:80.0) Gecko/20100101 Firefox/80.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 37
Origin: http://10.10.52.70
Connection: close
Referer: http://10.10.52.70/support/login/
Upgrade-Insecure-Requests: 1

username=§pentester§&password=§Expl01ted§
```

If we use Battering ram to attack this, Intruder will take each payload and substitute it into every position _at once._  

With the two positions that we have above, Intruder would use the three words from before (`burp`, `suite`, and `intruder`) to make _three_ requests:  

|**Request Number**|**Request Body**|
|---|---|
|1|`username=burp&password=burp`|
|2|`username=suite&password=suite`|
|3|`username=intruder&password=intruder`|

As can be seen in the table, each item in our list of payloads gets put into _every_ position for each request. True to the name, Battering ram just throws payloads at the target to see what sticks.

# Pitchfork

Two down, two more to go!

After Sniper, Pitchfork is the attack type you are most likely to use. It may help to think of Pitchfork as being like having numerous Snipers running simultaneously. Where Sniper uses _one_ payload set (which it uses on every position simultaneously), Pitchfork uses one payload set per position (up to a maximum of 20) and iterates through them all at once.

This type of attack can take a little time to get your head around, so let's use our bruteforce example from before, but this time we need two wordlists:

- Our first wordlist will be usernames. It contains three entries: `joel`, `harriet`, `alex`.
- Let's say that Joel, Harriet, and Alex have had their passwords leaked: we know that Joel's password is `J03l`, Harriet's password is `Emma1815`, and Alex's password is `Sk1ll`.  

We can use these two lists to perform a pitchfork attack on the login form from before. The process for carrying out this attack will not be covered in this task, but you will get plenty of opportunities to perform attacks like this later!

When using Intruder in pitchfork mode, the requests made would look something like this:

|**Request Number**|**Request Body**|
|---|---|
|1|`username=joel&password=J03l`|
|2|`username=harriet&password=Emma1815`|
|3|`username=alex&password=Sk1ll`|

See how Pitchfork takes the first item from each list and puts them into the request, one per position? It then repeats this for the next request: taking the second item from each list and substituting it into the template. Intruder will keep doing this until one (or all) of the lists run out. Ideally, our payload sets should be identical lengths when working in Pitchfork, as Intruder will stop testing as soon as one of the lists is complete. For example, if we have two lists, one with 100 lines and one with 90 lines, Intruder will only make 90 requests, and the final ten items in the first list will not get tested.

This attack type is exceptionally useful when forming things like credential stuffing attacks (we have just encountered a small-scale version of this). We will be looking more into these later in the room.

# Cluster Bomb

Finally, we come to the last of Intruder's attack types: the Cluster Bomb.

Like Pitchfork, Cluster bomb allows us to choose multiple payload sets: one per position, up to a maximum of 20; however, whilst Pitchfork iterates through each payload set simultaneously, Cluster bomb iterates through each payload set individually, making sure that every possible combination of payloads is tested.

Again, the best way to visualise this is with an example.

Let's use the same wordlists as before:
- Usernames: `joel`, `harriet`, `alex`.
- Passwords: `J03l`, `Emma1815`, `Sk1ll`.

But, this time, let's assume that we don't know which password belongs to which user. We have three users and three passwords, but we don't know how to match them up. In this case, we would use a cluster bomb attack; this will try _every_ combination of values. The request table for our username and password positions looks something like this:

|**Request Number**|**Request Body**|
|---|---|
|1|`username=joel&password=J03l`|
|2|`username=harriet&password=J03l`|
|3|`username=alex&password=J03l`|
|4|`username=joel&password=Emma1815`|
|5|`username=harriet&password=Emma1815`|
|6|`username=alex&password=Emma1815`|
|7|`username=joel&password=Sk1ll`|
|8|`username=harriet&password=Sk1ll`|
|9|`username=alex&password=Sk1ll`|

Cluster Bomb will iterate through every combination of the provided payload sets to ensure that every possibility has been tested. This attack-type can create a _huge_ amount of traffic (_equal to the number of lines in each payload set multiplied together_), so be careful! Equally, when using Burp Community and its Intruder rate-limiting, be aware that a Cluster Bomb attack with any moderately sized payload set will take an incredibly long time.

That said, this is another extremely useful attack type for any kind of credential bruteforcing where a username isn't known.

# Payloads

That was a lot of theory, so kudos for reading through it! There will be plenty of practicals in the upcoming tasks, but first, it is imperative that we understand how to create, assign, and use payloads.

Switch over to the "Payloads" sub-tab; this is split into four sections:
- The **Payload Sets** section allows us to choose which position we want to configure a set for as well as what type of payload we would like to use.
    - When we use an attack type that only allows for a single payload set (i.e. Sniper or Battering Ram), the dropdown menu for "Payload Set" will only have one option, regardless of how many positions we have defined.
    - If we are using one of the attack types that use multiple payload sets (i.e. Pitchfork or Cluster Bomb), then there will be one item in the dropdown for each position.  
        _**Note:** Multiple positions should be read from top to bottom, then left to right when being assigned numbers in the "Payload set" dropdown. For example, with two positions (_`username=§pentester§&password=§Expl01ted§`_), the first item in the payload set dropdown would refer to the username field, and the second would refer to the password field._  
        
    The second dropdown in this section allows us to select a "payload type". By default, this is a "Simple list" -- which, as the name suggests, lets us load in a wordlist to use. There are many other payload types available -- some common ones include: `Recursive Grep`, `Numbers`, and `Username generator`. It is well worth perusing this list to get a feel for the wide range of options available.  
- **Payload Options** differ depending on the payload type we select for the current payload set. For example, a "Simple List" payload type will give us a box to add and remove payloads to and from the set:

![](img/Pasted%20image%2020230828112256.png)

- We can do this manually using the "Add" text box, paste lines in with "Paste", or "Load..." from a file. The "Remove" button removes the currently selected line _only_. The "Clear" button clears the entire list. Be warned: loading extremely large lists in here can cause Burp to crash! By contrast, the options for a `Numbers` payload type allows us to change options such as the range of numbers used and the base that we are working with.  
- **Payload Processing** allows us to define rules to be applied to each payload in the set before being sent to the target. For example, we could capitalise every word or skip the payload if it matches a regex. You may not use this section particularly regularly, but you will definitely appreciate it when you _do_ need it!  
- Finally, we have the **Payload Encoding** section. This section allows us to override the default URL encoding options that are applied automatically to allow for the safe transmission of our payload. Sometimes it can be beneficial to _not_ URL encode these standard "unsafe" characters, which is where this section comes in. We can either adjust the list of characters to be encoded or outright uncheck the "URL-encode these characters" checkbox.  

When combined, these sections allow us to perfectly tailor our payload sets for any attack we wish to carry out.

# Practical example

We have covered a _lot_ of theory in the last section -- it is now past time that we put it all into practice.
Let's try to gain access to the support portal: `/support/login`.
This is a fairly typical login portal. Looking at the source code for the form, we can see that there are no protective measures in place:

Support Login Form Source Code
```html
---
<form method="POST">
    <div class="form-floating mb-3">
        <input class="form-control" type="text" name=username  placeholder="Username" required>
        <label for="username">Username</label>
    </div>
    <div class="form-floating mb-3">
        <input class="form-control" type="password" name=password  placeholder="Password" required>
        <label for="password">Password</label>
    </div>
    <div class="d-grid"><button class="btn btn-primary btn-lg" type="submit">Login!</button></div>
</form>
---
```
        

This lack of protective measures means that we could very easily attack this form using a cluster bomb attack for a bruteforce.

_But_, there is a much easier option available. Attached to this task (and available using `wget http://10.10.52.70:9999/Credentials/BastionHostingCreds.zip` for the sake of anyone using the AttackBox) is a list of leaked credentials for Bastion Hosting employees.

Bastion Hosting was hit with a cyber attack three months ago. The attack resulted in all of their employee usernames, emails, and plaintext passwords being leaked. Employees were told to change their passwords immediately; however, maybe one or two of them didn't listen...

As we have a list of known usernames, each associated with a password, we can avoid a straight bruteforce and instead use a credential stuffing attack. This will (blessedly) be much quicker when using the rate-limited version of Intruder.

Navigate to `http://10.10.52.70/support/login` in your browser.

Activate the Burp Proxy and try to log in, catching the request in your proxy.

Looking in the "Positions" sub-tab, we should see that the auto-selection should have chosen the username and password parameters, so we don't need to do anything else in terms of defining our positions. If you have already visited certain other pages on the site, then you may have a session cookie. If so, this will also be selected -- **make sure to clear your positions and select _only_ the username and passwords fields** if this happens to you.  

We also need the Attack type to be "Pitchfork":

![](img/Pasted%20image%2020230828114829.png)

Let's switch over to the "Payloads" sub-tab. We should find that we have two payload sets available:

![](img/Pasted%20image%2020230828114849.png)

Although these aren't named, we know from the fact that the username field is to the left of the password field that the first position will be for usernames, and the second position will be for passwords.

We can leave both of these as the "Simple list" payload type.  

In the first payload set, go to "Payload Options", choose "Load", then select our list of usernames.

Do the same thing for the second payload set and the list of passwords.

This process can be seen here:

![video demo](https://assets.muirlandoracle.co.uk/thm/modules/burp/settingPayloads.gif)

We have done all we need to do for this very simple attack, so go ahead and click the "Start Attack" button. A warning about the rate-limiting in Burp Community will appear. Click "Ok" and start the attack!

_**Note:** This will take a few minutes to complete in Burp Community -- hence the relatively small lists in use_

---

Once the attack has completed, we will be presented with a new window giving us the results -- but we have a new problem. Burp sent 100 requests: how are we supposed to know which one(s), if any, are valid?

The most common solution to this problem is to use the status code of the response to differentiate between successful or unsuccessful login attempts; this only works if there _is_ a difference in the status codes, however. Ideally, successful login requests would give us a 200 response code, and failed login requests would provide us with a 401; however, in many cases (this one included), we are just given a 302 redirect for all requests instead.

That solution is out.

The next most common solution is to use the _Length_ of the responses to identify differences between them. For example, a successful login attempt may have a response with 400 bytes in it, whereas an unsuccessful login attempt may yield a response with 600 bytes in it.

We can sort by byte length by clicking on the header for the "Length" column:

![](img/Pasted%20image%2020230828114941.png)

As you may have guessed, the request with the shorter response length was made with the valid credentials -- a fact we can confirm by attempting to log in with the credentials used in the successful request.

_**Note:** These are selected randomly from the list at machine boot and so will be different every time you deploy a new instance of the machine._

Well done, you have successfully bruteforced the support login page with a credential stuffing attack!

# Challenge
In the previous task, we gained access to the support system. Now it's time to see what we can do with it!

The home interface shows us a table of tickets -- if we click on any of the rows in the table, we get redirected to a page where we can view the full ticket. Looking at the URL, we can see that these pages are numbered, e.g.:  
`http://10.10.52.70/support/ticket/NUMBER`  

So, what does this mean?

The numbering means that we know the tickets aren't being identified by hard-to-guess IDs -- they are simply assigned an integer identifier.

What happens if we use intruder to fuzz the`/support/ticket/NUMBER`  endpoint? One of two things will happen:
1. The endpoint has been set up correctly only to allow us to view tickets that are assigned to our current user, or
2. The endpoint has _not_ had the correct access controls set, which would allow us to read all of the existing tickets! If this is the case, then a vulnerability called an IDOR (**I**nsecure **D**irect **O**bject **R**eferences) is present.  

Let's try fuzzing this endpoint!

Configure an appropriate position and payload (the tickets are stored at values between 1 and 100), then start the attack.

# CSRF Token Bypass
Let's crank this up a notch with an extra mile exercise. This challenge will be a slightly harder variant of the credential stuffing attack that we carried out a few tasks ago -- only this time there will be measures in place to make bruteforcing harder. If you are comfortable using Burp Macros, please feel free to do this challenge blind; otherwise, read on!

---

Let's start by catching a request to `http://10.10.52.70/admin/login/` and reviewing the response:

```html
HTTP/1.1 200 OK
Server: nginx/1.18.0 (Ubuntu)
Date: Fri, 20 Aug 2021 22:31:16 GMT
Content-Type: text/html; charset=utf-8
Connection: close
Set-Cookie: session=eyJ0b2tlbklEIjoiMzUyNTQ5ZjgxZDRhOTM5YjVlMTNlMjIzNmI0ZDlkOGEifQ.YSA-mQ.ZaKKsUnNsIb47sjlyux_LN8Qst0; HttpOnly; Path=/
Vary: Cookie
Front-End-Https: on
Content-Length: 3922
---
<form method="POST">
    <div class="form-floating mb-3">
        <input class="form-control" type="text" name=username  placeholder="Username" required>
        <label for="username">Username</label>
    </div>
    <div class="form-floating mb-3">
        <input class="form-control" type="password" name=password  placeholder="Password" required>
        <label for="password">Password</label>
    </div>
    <input type="hidden" name="loginToken" value="84c6358bbf1bd8000b6b63ab1bd77c5e">
    <div class="d-grid"><button class="btn btn-warning btn-lg" type="submit">Login!</button></div>
</form>
```

We have the same username and password fields as before, but now there is also a session cookie set in the response, as well as a CSRF (**C**ross-**S**ite **R**equest **F**orgery) token included in the form as a hidden field. If we refresh the page, we should see that both of these change with each request: this means that we will need to extract valid values for both _every time we make a request._

In other words, every time we attempt to log in, we will need unique values for the session cookie and `loginToken` hidden form input.

Enter: Macros.

In many cases, we could do this kind of thing using a payload type called "Recursive Grep", which would be a lot easier than what we're going to have to do here. Unfortunately, because the web app redirects us back to the login page rather than simply showing us both of our target parameters, we will need to do this the hard way.  Specifically, we will have to define a "macro" (i.e. a short set of repeated actions) to be executed before each request. This will grab a unique session cookie and matching login token, then substitute them into each request of our attack.

Before we get into the tricky stuff, let's deal with what we know.

Navigate to  `http://10.10.52.70/admin/login/`.

Activate the Burp Proxy and attempt to log in. Capture the request and send it to Intruder.

Configure the positions the same way as we did for bruteforcing the support login:
- Set the attack type to be "Pitchfork".
- Clear all of the predefined positions and select _only_ the username and password form fields. The other two positions will be handled by our macro.

![](img/Pasted%20image%2020230828120232.png)

Now switch over to the Payloads sub-tab and load in the same username and password wordlists we used for the support login attack.

Up until this point, we have configured Intruder in almost the same way as our previous credential stuffing attack; this is where things start to get more complicated.

---

With the username and password parameters handled, we now need to find a way to grab the ever-changing loginToken and session cookie. Unfortunately, Recursive Grep won't work here due to the redirect response, so we can't do this entirely within Intruder -- we will need to build a macro.

Macros allow us to perform the same set of actions repeatedly. In this case, we simply want to send a GET request to `/admin/login/`.

Fortunately, setting this up is a very easy process.
- Switch over to the "Project Options" tab, then the "Sessions" sub-tab.
- Scroll down to the bottom of the sub-tab to the "Macros" section and click the "Add" button.
- The menu that appears will show us our request history. If there isn't a GET request to `http://10.10.52.70/admin/login/` in the list already, navigate to this location in your browser and you should see a suitable request appear in the list.
- With the request selected, click Ok.
- Finally, give the macro a suitable name, then click "Ok" again to finish the process.

There are a lot of steps here, comparatively speaking, so the following GIF shows the entire process:

![video demo](https://assets.muirlandoracle.co.uk/thm/modules/burp/creatingMacro.gif)

Now that we have a macro defined, we need to set Session Handling rules that define how the macro should be used.
- Still in the "Sessions" sub-tab of Project Options, scroll up to the "Session Handling Rules" section and choose to "Add" a new rule.
- A new window will pop up with two tabs in it: "Details" and "Scope". We are in the Details tab by default.

![](img/Pasted%20image%2020230828120413.png)

- Fill in an appropriate description, then switch over to the Scope tab.
- In the "Tools Scope" section, deselect every checkbox other than Intruder -- we do not need this rule to apply anywhere else.
- In the "URL Scope" section, choose "Use suite scope"; this will set the macro to only operate on sites that have been added to the global scope (as was discussed in [Burp Basics](https://tryhackme.com/room/burpsuitebasics)). If you have not set a global scope, keep the "Use custom scope" option as default and add `http://10.10.52.70/` to the scope in this section.

![](img/Pasted%20image%2020230828120431.png)

Again, here is a GIF showing these steps of the process:

![video demo](https://assets.muirlandoracle.co.uk/thm/modules/burp/configuringSessionHandlerP1.gif)

Now we need to switch back over to the Details tab and look at the "Rule Actions" section.
- Click the "Add" button -- this will cause a dropdown menu to appear with a list of actions we can add.
- Select "Run a Macro" from this list.
- In the new window that appears, select the macro we created earlier.

As it stands, this macro will now overwrite all of the parameters in our Intruder requests before we send them; this is great, as it means that we will be getting the loginTokens and session cookies added straight into our requests. That said, we should restrict which parameters and cookies are being updated before we start our attack:
- Select "Update only the following parameters", then click the "Edit" button next to the input box below the radio button.  
- In the "Enter a new item" text field, type "loginToken". Press "Add", then "Close".
- Select "Update only the following cookies", then click the relevant "Edit" button.
- Enter "session" in the "Enter a new item" text field, press "Add", then "Close".
- Finally, press "Ok" to confirm our action.

The following GIF demonstrates this final stage of the process:

![video demo](https://assets.muirlandoracle.co.uk/thm/modules/burp/addingRuleAction.gif)

Click "Ok", and we're done!

---

Phew, that was a long process!

You should now have a macro defined that will substitute in the CSRF token and session cookie. All that's left to do is switch back to Intruder and start the attack!

_**Note:** You should be getting 302 status code responses for every request in this attack. If you see 403 errors, then your macro is not working properly._

As with the support login credential stuffing attack we carried out, the response codes here are all the same (302 Redirects). Once again, order your responses by Length to find the valid credentials. Your results won't be quite as clear-cut as last time -- you will see quite a few different response lengths: however, the response that indicates a successful login should still stand out as being quite significantly shorter.

Use the credentials you just found to log in (you may need to refresh the login page before entering the credentials).