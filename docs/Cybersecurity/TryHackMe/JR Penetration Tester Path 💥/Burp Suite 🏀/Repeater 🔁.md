# What is Repeater?
Before we start using Repeater, it will help to have a good idea of what it does.

In short: Burp Suite Repeater allows us to craft and/or relay intercepted requests to a target at will. In layman's terms, it means we can take a request captured in the Proxy, edit it, and send the same request repeatedly as many times as we wish. Alternatively, we could craft requests by hand, much as we would from the CLI (**C**ommand **L**ine **I**nterface), using a tool such as [cURL](https://curl.se/) to build and send requests.

This ability to edit and resend the same request multiple times makes Repeater ideal for any kind of manual poking around at an endpoint, providing us with a nice **G**raphical **U**ser **I**nterface (GUI) for writing the request payload and numerous views (including a rendering engine for a graphical view) of the response so that we can see the results of our handiwork in action.  

---

The Repeater interface can be split into six main sections -- an annotated diagram can be found below the following bullet points:
1. At the very top left of the tab, we have a list of Repeater requests. We can have many different requests going through Repeater: each time we send a new request to Repeater, it will appear up here.
2. Directly underneath the request list, we have the controls for the current request. These allow us to send a request, cancel a hanging request, and go forwards/backwards in the request history.
3. Still on the left-hand side of the tab, but taking up most of the window, we have the request and response view. We edit the request in the Request view then press send. The response will show up in the Response view.
4. Above the request/response section, on the right-hand side, is a set of options allowing us to change the layout for the request and response views. By default, this is usually side-by-side (horizontal layout, as in the screenshot); however, we can also choose to put them above/below each other (vertical layout) or in separate tabs (combined view).
5. At the right-hand side of the window, we have the Inspector, which allows us to break requests apart to analyse and edit them in a slightly more intuitive way than with the raw editor. We will cover this in a later task.
6. Finally, above the Inspector we have our target. Quite simply, this is the IP address or domain to which we are sending requests. When we send requests to Repeater from other parts of Burp Suite, this will be filled in automatically.

![](./img/Pasted%20image%2020230825115317.png)

Don't worry if this doesn't make too much sense just now -- you will get plenty of chances to learn what it does first hand in the upcoming tasks!

# Basic Usage
We know what the interface looks like now, but how do we put it to use?

Whilst we _can_ craft requests by hand, it would be much more common to simply capture a request in the Proxy, then send that through to Repeater for editing/resending.

With a request captured in the proxy, we can send to repeater either by right-clicking on the request and choosing "Send to Repeater" or by pressing `Ctrl + R`.

Switching back to Repeater, we can see that our request is now available:

![](./img/Pasted%20image%2020230825115743.png)

The target and Inspector elements are now also showing information; however, we do not yet have a response. When we click the "Send" button, the Response section quickly populates:

![](./img/Pasted%20image%2020230825115804.png)

If we want to change anything about the request, we can simply type in the Request window and press "Send" again; this will update the Response on the right. For example, changing the "Connection" header to `open` rather than `close` results in a response "Connection" header with a value of `keep-alive`:

![](./img/Pasted%20image%2020230825115822.png)

We could then also use the history buttons to the right of the Send button to go forwards and backwards in our modification history.

# Views
Repeater offers us various ways to present the responses to our requests -- these range from hex output all the way up to a fully rendered version of the page.

We can see the available options by looking above the response box:

![](./img/Pasted%20image%2020230825120527.png)

We have four display options here:

1. **Pretty:** This is the default option. It takes the raw response and attempts to beautify it slightly, making it easier to read.
2. **Raw:** The pure, un-beautified response from the server.
3. **Hex:** This view takes the raw response and gives us a byte view of it -- especially useful if the response is a binary file.
4. **Render:** The render view renders the page as it would appear in your browser. Whilst not _hugely_ useful given that we would usually be interested in the source code when using Repeater, this is still a neat trick.

In most instances, the "Pretty" option is perfectly adequate; however, it is still well worth knowing how to use the other three options.

---

Just to the right of the view buttons is the "Show non-printable characters" button (`\n`). This button allows us to display characters that usually wouldn't show up in the Pretty or Raw views. For example, every line in the response will end with the characters `\r\n` -- these signify a carriage return followed by a newline and are part of how HTTP headers are interpreted.  

Whilst not required for most tasks, this option can still come in handy.

# Inspector
In many ways, Inspector is entirely supplementary to the request and response fields of the Repeater window. If you understand how to read and edit HTTP requests, then you may find that you rarely use Inspector at all.

That said, it is a superb way to get a prettified breakdown of the requests and responses, as well as for experimenting to see how changes made using the higher-level Inspector affect the equivalent raw versions.

Inspector can be used in the Proxy as well as Repeater. In both cases, it appears over at the very right hand side of the window and gives us a list of the components in the request and response:

![](./img/Pasted%20image%2020230825120737.png)

Of these, the request sections can nearly always be altered, allowing us to add, edit, and delete items. For example, in the Request Attributes section, we can edit the parts of the request that deal with location, method and protocol; e.g. changing the resource we are looking to retrieve, altering the request from GET to another HTTP method, or switching protocol from HTTP/1 to HTTP/2:

![](./img/Pasted%20image%2020230825120754.png)

The other sections available for viewing and/or editing are:  
- **Query Parameters**, which refer to data being sent to the server in the URL. For example, in a GET request to `https://admin.tryhackme.com/?redirect=false`, there is a query parameter called "redirect" with a value of "false".  
- **Body Parameters**, which do the same thing as Query Parameters, but for POST requests. Anything that we send as data in a POST request will show up in this section, once again allowing us to modify the parameters before re-sending.
- **Request Cookies** contain, as you may expect, a modifiable list of the cookies which are being sent with each request.
- **Request Headers** allow us to view, access, and modify (including outright adding or removing) any of the headers being sent with our requests. Editing these can be very useful when attempting to see how a webserver will respond to unexpected headers.  
- **Response Headers** show us the headers that the server sent back in response to our request. These cannot be edited (as we can't control what headers the server returns to us!). Note that this section will only show up after we have sent the request and received a response.  

These components can all be found as text within the request and response sections; however, it can be nice to see them in the tabular format offered by Inspector. It is well worth adding, removing, and editing headers in Inspector to get a feel for how the raw version changes as you do so.

# Sqli with Repeater
This task contains an extra-mile challenge, which means that it is a slightly harder, real-world application for Burp Repeater. If you feel comfortable performing a manual SQL Injection by yourself, you may skip to the last question and try this as a blind challenge; otherwise a guide will be given below.  

Before we start on this challenge: if you don't already know the principles of SQLi, then it would be well worth your time checking out the [room on the topic](https://tryhackme.com/jr/sqlinjectionlm); however, full steps will be provided, so you do not need in-depth knowledge of the principles behind SQL Injection to complete this task.

---

The brief is as follows:

_There is a Union SQL Injection vulnerability in the ID parameter of the_ `/about/ID` _endpoint. Find this vulnerability and execute an attack to retrieve_ _the notes about the CEO stored in the database._

We know that there is a vulnerability, and we know where it is. Now we just need to exploit it!

Let's start by capturing a request to `http://10.10.213.11/about/2` in the Burp Proxy. Once you have captured the request, send it to Repeater with `Ctrl + R` or by right-clicking and choosing "Send to Repeater".

Now that we have our request primed, let's confirm that a vulnerability exists. Adding a single apostrophe (`'`) is usually enough to cause the server to error when a simple SQLi is present, so, either using Inspector or by editing the request path manually, add an apostrophe after the "2" at the end of the path and send the request:

```
GET /about/2' HTTP/1.1
Host: 10.10.213.11
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:80.0) Gecko/20100101 Firefox/80.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1
```

You should see that the server responds with a "500 Internal Server Error", indicating that we successfully broke the query:

```html
HTTP/1.1 500 INTERNAL SERVER ERROR<
Server: nginx/1.18.0 (Ubuntu)
Date: Mon, 16 Aug 2021 23:05:21 GMT
Content-Type: text/html; charset=utf-8
Content-Length: 3101
```

If we look through the body of the server's response, we see something very interesting at around line 40. The server is telling us the query we tried to execute:

```html
<h2>
    <code>Invalid statement: 
        <code>SELECT firstName, lastName, pfpLink, role, bio FROM people WHERE id = 2'</code>
    </code>
</h2>
```

This is an extremely useful error message which the server should absolutely not be sending us, _but_ the fact that we have it makes our job significantly more straightforward.

The message tells us a couple of things that will be invaluable when exploiting this vulnerability:
- The database table we are selecting from is called people.
- The query is selecting _five_ columns from the table: `firstName`, `lastName`, `pfpLink`, `role`, and `bio`. We can guess where these fit into the page, which will be helpful for when we choose where to place our responses.

With this information, we can skip over the query column number and table name enumeration steps.

Although we have managed to cut out a lot of the enumeration required here, we still need to find the name of our target column.

As we know the table name and the number of rows, we can use a union query to select the column names for the `people` table from the `columns` table in the `information_schema` default database.

A simple query for this is as follows:  
`/about/0 UNION ALL SELECT column_name,null,null,null,null FROM information_schema.columns WHERE table_name="people"`  

This creates a union query and selects our target then four null columns (to avoid the query erroring out). Notice that we also changed the ID that we are selecting from `2` to `0`. By setting the ID to an invalid number, we  ensure that we don't retrieve anything with the original (legitimate) query; this means that the first row returned from the database will be our desired response from the injected query.

Looking through the returned response, we can see that the first column name (`id`) has been inserted into the page title:

```html
HTTP/1.1 200 OK
Server: nginx/1.18.0 (Ubuntu)
Date: Mon, 16 Aug 2021 22:12:36 GMT
Content-Type: text/html; charset=utf-8
Connection: close
Front-End-Https: on
Content-Length: 3360


<!DOCTYPE html>
<html lang=en>
    <head>
        <title>
            About | id None
        </title>
-----
```

We have successfully pulled the first column name out of the database, but we now have a problem. The page is only displaying the _first_ matching item -- we need to see _all_ of the matching items.

Fortunately, we can use our SQLi to group the results. We can still only retrieve one result at a time, but by using the `group_concat()` function, we can amalgamate all of the column names into a single output:  
`/about/0 UNION ALL SELECT group_concat(column_name),null,null,null,null FROM information_schema.columns WHERE table_name="people"`  

This process is shown in below:

![](./img/Pasted%20image%2020230825123813.png)

We have successfully identified eight columns in this table: `id`, `firstName`, `lastName`, `pfpLink`, `role`, `shortRole`, `bio`, and `notes`.

Considering our task, it seems a safe bet that our target column is `notes`.

Finally, we are ready to take the flag from this database -- we have all of the information that we need:
- The name of the table: `people`.
- The name of the target column: `notes`.
- The ID of the CEO is `1`; this can be found simply by clicking on Jameson Wolfe's profile on the `/about/` page and checking the ID in the URL.

Let's craft a query to extract this flag:  
`0 UNION ALL SELECT notes,null,null,null,null FROM people WHERE id = 1   `

Hey presto, we have a flag!

![](./img/Pasted%20image%2020230825123841.png)


