# GitHub API Tutorial

Build a simple web application by learning the fundamentals of the GitHub API and then display dynamic data to the front-end!

![GitHub API Tutorial](https://images.unsplash.com/photo-1555066931-4365d14bab8c?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxMTc3M3wwfDF8c2VhcmNofDR8fGNvZGV8ZW58MHx8fHwxNjY3NTI0Nzcw&ixlib=rb-4.0.3&q=80&w=1200)

Photo by [Arnold Francisca](https://unsplash.com/@clark_fransa?utm_source=ghost&utm_medium=referral&utm_campaign=api-credit) / [Unsplash](https://unsplash.com/?utm_source=ghost&utm_medium=referral&utm_campaign=api-credit)

GitHub is one of the best ways to collaborate on software and discover new projects using Git, the popular [Version Control System (VCS)](https://en.wikipedia.org/wiki/Version_control). It's safe to say that GitHub is a huge part of the [Open Source Software](https://en.wikipedia.org/wiki/Open-source_software) movement that is continually pushing the bounds of technology as we know it by helping developers contribute to more projects and network with other developers.

GitHub has also created an awesome [API](https://simple.wikipedia.org/wiki/Application_programming_interface) for us to build applications with, and the good news is that it's really easy to get started.

🙌

This tutorial has been updated to use (the more conventional) `fetch` method to send network requests instead of `XmlHttpRequest`. If you would prefer to use `XmlHttpRequest` please follow the original tutorial [here](https://codesnippet.io/github-api-tutorial-original/).

## Using the GitHub API

Let's take a look at how we can start working with [GitHub's REST API](https://docs.github.com/en/rest). Click [here](https://docs.github.com/en/rest/overview/endpoints-available-for-github-apps) for a comprehensive list of available GitHub API endpoints.

For today's example will make use of the [`GET /users/<username>/repos`](https://docs.github.com/en/rest/repos/repos#list-repositories-for-a-user) endpoint which will allow us to list all public repositories for the specified `<username>` parameter. This is a simple API endpoint for us to test the waters with.

In fact, we can actually just paste the url below into a web browser and observe some data 🤯.

👉

Try it out: `[https://api.github.com/users/timmywheels/repos](https://api.github.com/users/timmywheels/repos)`

If everything went well, you should see the first 30 public repositories for my GitHub username, `timmywheels`. If you're feeling daring, try using your GitHub username instead!

![codesnippet-github-api-example](https://codesnippet.io/content/images/2018/11/codesnippet-github-api-example.png)

👉

The reason pasting this URL into a browser _just works_ is because the browser implicitly sends a HTTP `[GET](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/GET)` request when a URL is entered. Pretty cool!

🔥

_**p.s.**_ I'm using the [JSONView Chrome Extension](https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc?hl=en) to pretty-print the JSON output in my browser.

### Requesting Resources from GitHub's API Using `fetch`

There are a number of ways to request data [asynchronously](https://developer.mozilla.org/en-US/docs/Glossary/Asynchronous) from a backend server, but today we'll use the built-in JavaScript [`fetch`](https://developer.mozilla.org/en-US/docs/Web/API/fetch) method. As we will soon see, getting started with `fetch` is pretty straightforward.

⚠️

An earlier version of this post used `XMLHttpRequest` to request backend resources, but using `fetch` is a lot more common.

### Create a Function to Call GitHub's API

First things first, let's create a simple function that will ultimately wrap the `fetch` request to GitHub's `/users/<username>/repos`, where `<username>` is a dynamic value.

Given that `<username>` is dynamic, we'll want to make sure we pass a `username` argument to our function.

```javascript

function requestUserRepos(username){
  // we'll fill this in later
}
```

JavaScript

### Use `fetch` to request data from GitHub

Let's add our `fetch` request to the function we just created above.

```javascript
function requestUserRepos(username){
    // call the fetch method, 
    // passing in the `username` arg to the request
    fetch(`https://api.github.com/users/${username}/repos`);
}
```

JavaScript

### Working with [`Promises`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)

If you were to invoke `requestUserRepos(someUsername)`, you wouldn't see much just yet. **That's because when we call `fetch`, it returns a [`Promise`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)** which is...

> [an] object [that] represents the eventual completion (or failure) of an asynchronous operation and its resulting value.

Ultimately, a `Promise` is a guarantee that an asynchronous operation will complete _at some unknown point in the future_. `Promise`s are particularly useful when dealing with network requests because we don't know when the data will be returned from GitHub (or any API for that matter), but they provide a declaritive way in which our code can handle the various states of a `Promise`.

A `Promise` will always be in 1 of these 3 states:

-   `pending`: The initial state
-   `fulfilled`: The operation was successful
-   `rejected`: The operation failed

### Parsing the `Promise` returned from `fetch`

There are a number of ways to leverage `Promise`s in JavaScript. We will make use of the `Promise.then()` methods which (admittedly) makes the code a little more verbose, but it allows us to work directly from the comfort of our [browser console](https://codesnippet.io/console/).

⚠️

In today's JavaScript landscape, it's generally preferred to use `async` / `await` syntax as it's more straightforward and easier to read. **However**, since this is an interactive tutorial designed to be followed through the [browser console](https://codesnippet.io/console/), I have decided to forgo async/await since this tutorial would largely need to rely on [IIFEs](https://developer.mozilla.org/en-US/docs/Glossary/IIFE) (when running in the console)

```javascript
function requestUserRepos(username){
    // create a variable to hold the `Promise` returned from `fetch`
    return Promise.resolve(fetch(`https://api.github.com/users/${username}/repos`));
}

// call function, passing in any GitHub username as an arg
requestUserRepos('facebook')
  // parse response into json
  .then(response => response.json())
  // log response data
  .then(data => console.log(data));
  
  // iterate through parsed response
  .then(data => {
    // Log the repo name
    console.log('Repo:', data[i].name);

    // Log the repo description
    console.log('Description:', data[i].description);

    // Log the repo url
    console.log('URL:', data[i].html_url);

    // Add a separator between each repo
    console.log('=========================') 
})
```

JavaScript

☝️

Try this in your [browser console](https://codesnippet.io/console/)

### Viewing the Entire API Response

After running the code above, you will see a response that returns an array of 30 objects. Each object contains information about a particular repository. GitHub's API, by default, is set to return the first 30 repos for that particular user in alphabetical order.

You should see something similar to this:  
![codesnippet-github-api-result](https://codesnippet.io/content/images/2018/11/codesnippet-github-api-result.png)

👏

Awesome! We're now working with the GitHub API. With that said, let's keep it moving and see how we can access some more information using our API request that we have in place.

### Iterating Through the Payload

Let's say that we wanted to retrieve the **name**, **description**, and **url** for each repo that is returned in the response payload.

You'll notice that if you expand the individual objects from the response payload, they contain all of the information that we're looking for. In our case, we'll want to somehow grab the `name`, `description`, and `html_url` keys from each object within the `data` array.

![codesnippet-github-api-response-object](https://codesnippet.io/content/images/2018/11/codesnippet-github-api-response-object.png)

Instead of logging the entire `data` payload as we did previously, let's be a little more intentional and log the `name`, `description`, and `html_url` for each individual repository like so:

```javascript
// call function, passing in any GitHub username as an arg
requestUserRepos('facebook')
  // parse response into json
  .then(response => response.json())
  // iterate through parsed response
  .then(data => {
    // Log the repo name
    console.log('Repo:', data[i].name);

    // Log the repo description
    console.log('Description:', data[i].description);

    // Log the repo url
    console.log('URL:', data[i].html_url);

    // Add a separator between each repo
    console.log('=========================') 
})
```

JavaScript

### Viewing the Requested API Data 👀

Nice! Now we have our GitHub API data formatted into something that's a little easier to read.

![codesnippet-github-api-formatted-data-001](https://codesnippet.io/content/images/2018/11/codesnippet-github-api-formatted-data-001.png)

## So Now What?

Now that we've setup our GitHub API request, we'd naturally want to display this somewhere to the users of our application, and not just in the [browser console](https://codesnippet.io/console). So how do we do that?

## Creating a Simple GitHub API Example Application

Let's setup a simple project that will display the data of the specified username right on our webpage.

### 1. Create directory named `github-api` on your desktop

Let's create directory on our desktop named `github-api` which will hold the files to our simple GitHub API example application.

### 2. Within `github-api` directory, add file `index.html`

This file will contain the HTML markup for our web app.

### 3. Within `github-api` directory, add file `app.js`

This file will contain the code we just wrote. We will tweak it along the way to get it to display the requested data on the webpage.

![codesnippet-github-api-example-folder-structure](https://codesnippet.io/content/images/2018/11/codesnippet-github-api-example-folder-structure.png)

### Our `index.html` file

This one will be pretty straight forward. Just some simple HTML boilerplate with an `h3`, a `form`, a `ul`, and a link to the `app.js` file.

Just to spice things up, we will also import the [Bootstrap CSS Library](https://getbootstrap.com/) and add a few Bootstrap classes to our HTML elements.

ℹ️

Bootstrap is not necessary to get your GitHub app working, but for the sake of making it look half decent, we'll add it to our project.

###### We will use the Bootstrap CSS CDN:

You can find the docs for the CDN here: [https://getbootstrap.com/docs/4.1/getting-started/introduction/](https://getbootstrap.com/docs/4.1/getting-started/introduction/)

```html
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css" integrity="sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO" crossorigin="anonymous">
```

HTML

###### We will use a few common Bootstrap classes:

I have linked to the corresponding sections of the Bootstrap documentation for each of the classes here.

-   `.text-center` | Used for text alignment | [View Documentation](https://getbootstrap.com/docs/4.1/utilities/text/#text-alignment)
-   `.mt-5`, `.mx-auto`, `.mb-5`, `.ml-2` | Used for margins | [View Documentation](https://getbootstrap.com/docs/4.1/layout/utilities-for-layout/#margin-and-padding)
-   `.form-inline` | Used for making form fields inline | [View Documentation](https://getbootstrap.com/docs/4.1/components/forms/#inline-forms)
-   `.form-control` | Used for general appearance of form fields | [View Documentation](https://getbootstrap.com/docs/4.1/components/forms/#form-controls)
-   `.btn` | Used for general appearance of buttons | [View Documentation](https://getbootstrap.com/docs/4.1/components/buttons/#button-tags)
-   `.btn-primary` | Button appearance modifier class | [View Documentation](https://getbootstrap.com/docs/4.1/extend/approach/#classes)
-   `.list-group` | General unordered list styling | [View Documentation](https://getbootstrap.com/docs/4.1/components/list-group/#basic-example)
-   `.list-group-item` | General unordered list item styling | [View Documentation](https://getbootstrap.com/docs/4.1/components/list-group/#basic-example)

ℹ️

FYI - the `.list-group-item` class is only used in `app.js` – not `index.html`

All in all, there's not much to the Bootstrap classes I've added to this app, however, I wanted to make sure to get you started off on the right track. From here you can certainly put your own spin on things and truly make it your own.

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>GitHub API</title>

	<!-- Import the Bootstrap CSS CDN -->
	<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css" integrity="sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO" crossorigin="anonymous">

</head>
<body>

	<h3 class="text-center mt-5">GitHub API</h3>
	<form id="gitHubForm" class="form-inline mx-auto" style="width: 280px">
		<input id="usernameInput" class="form-control mb-5" type="text" name="username" placeholder="GitHub Username">
		<input type="submit" class="btn btn-primary ml-2 mb-5" value="Submit">
	</form>
	<ul id="userRepos" class="list-group mx-auto mb-5" style="width: 500px">

	</ul>
	
	<script src="app.js"></script>
</body>
</html>
```

HTML

### Our `app.js` file

This will be mostly similar to the code we wrote earlier. The main differences will be that we need to retrieve the user's input from the GitHub username form, and pass that into our `requestUserRepos()` function from earlier, then we need to attach the data from our API request to the DOM. We can do this by grabbing on to the `ul` with an ID of `userRepos` and appending the data as `li`'s within the `ul` all from within the for-loop inside the final `.then()` method on `requestUserRepos`. Let's give it a shot:

```javascript
// Get the GitHub username input form
const gitHubForm = document.getElementById('gitHubForm');

// Listen for submissions on GitHub username input form
gitHubForm.addEventListener('submit', (e) => {

    // Prevent default form submission action
    e.preventDefault();

    // Get the GitHub username input field on the DOM
    let usernameInput = document.getElementById('usernameInput');

    // Get the value of the GitHub username input field
    let gitHubUsername = usernameInput.value;

    // Run GitHub API function, passing in the GitHub username
    requestUserRepos(gitHubUsername)
        // resolve promise then parse response into json
        .then(response => response.json())
        // resolve promise then iterate through json
        .then(data => {
            // update html with data from github
            for (let i in data) {
                // Get the ul with id of userRepos

                if (data.message === "Not Found") {
                    let ul = document.getElementById('userRepos');

                    // Create variable that will create li's to be added to ul
                    let li = document.createElement('li');

                    // Add Bootstrap list item class to each li
                    li.classList.add('list-group-item')
                    // Create the html markup for each li
                    li.innerHTML = (`
                <p><strong>No account exists with username:</strong> ${gitHubUsername}</p>`);
                    // Append each li to the ul
                    ul.appendChild(li);
                } else {

                    let ul = document.getElementById('userRepos');

                    // Create variable that will create li's to be added to ul
                    let li = document.createElement('li');

                    // Add Bootstrap list item class to each li
                    li.classList.add('list-group-item')

                    // Create the html markup for each li
                    li.innerHTML = (`
                <p><strong>Repo:</strong> ${data[i].name}</p>
                <p><strong>Description:</strong> ${data[i].description}</p>
                <p><strong>URL:</strong> <a href="${data[i].html_url}">${data[i].html_url}</a></p>
            `);

                    // Append each li to the ul
                    ul.appendChild(li);
                }
            }
        })
})

function requestUserRepos(username) {
    // create a variable to hold the `Promise` returned from `fetch`
    return Promise.resolve(fetch(`https://api.github.com/users/${username}/repos`));
}
```

JavaScript

## Trying Out Our GitHub API App

Now that we've put together all of our code for the front-end markup, our API request, and added some Bootstrap styling - we should be ready to rock.

All you have to do is open up the `index.html` file in your browser. On a Mac, you can just double-click the file itself, or right-click > Open With > Google Chrome.

### Our Simple App UI

And there it is! Here's what all of our hardworks gone into. This will give you a great framework to build upon and expand your app.

![codesnippet-github-api-app-ui](https://codesnippet.io/content/images/2018/11/codesnippet-github-api-app-ui.png)

### Enter a GitHub Username

Now for the fun part. Enter your GitHub username or even ones like `facebook`, `airbnb`, `reactjs`, or mine - `timmywheels`.

Here's the results I got when I plugged in `facebook`:

![codesnippet-github-api-example-app-ui](https://codesnippet.io/content/images/2018/11/codesnippet-github-api-example-app-ui.png)

## Congratulations, Hacker!

You have successfully built a web application that makes a request to the GitHub API and displays dynamic data to users on the front-end inside the browser! Really cool stuff.

---