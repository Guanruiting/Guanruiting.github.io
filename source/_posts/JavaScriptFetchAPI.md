---
title: How To Use the JavaScript Fetch API to Get Data
time: 2020-12-23 10:55:00
tags:
- Javascript
- Fetch
categories: English
---

### Introduction

There was a time when `XMLHttpRequest` was used to make API requests. It didn’t include promises, and it didn’t make for clean JavaScript code. Using jQuery, you used the cleaner syntax with `jQuery.ajax()`.

Now, JavaScript has its own built-in way to make API requests. This is the Fetch API, a new standard to make server requests with promises, but includes many other features.

In this tutorial, you will create both GET and POST requests using the Fetch API.

<!--more-->

## Prerequisites

To complete this tutorial, you will need the following:

- The latest version of Node installed on your machine. To install Node on macOS, follow the steps outlined in this [How to Install Node.js and Create a Local Development Environment on macOS](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-and-create-a-local-development-environment-on-macos) tutorial.
- A basic understanding of coding in JavaScript, which you can learn more about from the [How to Code in JavaScript](https://www.digitalocean.com/community/tutorial_series/how-to-code-in-javascript) series.
- An understanding of promises in JavaScript. Read the [Promises section](https://www.digitalocean.com/community/tutorials/understanding-the-event-loop-callbacks-promises-and-async-await-in-javascript#promises) of this article on [the event loop, callbacks, promises, and async/await](https://www.digitalocean.com/community/tutorials/understanding-the-event-loop-callbacks-promises-and-async-await-in-javascript) in JavaScript.

## Step 1 — Getting Started with Fetch API Syntax

To use the Fetch API, call the `fetch` method, which accepts the URL of the API as a parameter:

```javascript
fetch(url)
```

After the `fetch()` method, include the promise method `then()`:

```javascript
.then(function() {

})
```

The `fetch()` method returns a promise. If the promise returned is `resolve`, the function within the `then()` method is executed. That function contains the code for handling the data received from the API.

Below the `then()` method, include the `catch()` method:

```javascript
.catch(function() {

});
```

The API you call using `fetch()` may be down or other errors may occur. If this happens, the `reject` promise will be returned. The `catch` method is used to handle `reject`. The code within `catch()` will be executed if an error occurs when calling the API of your choice.

To summarize, using the Fetch API will look like this:

```javascript
fetch(url)
.then(function() {

})
.catch(function() {

});
```

With an understanding of the syntax for using the Fetch API, you can now move on to using `fetch()` on a real API.

## Step 2 — Using Fetch to get Data from an API

The following code samples will be based on the [Random User API](https://randomuser.me/). Using the API, you will get ten users and display them on the page using Vanilla JavaScript.

The idea is to get all the data from the Random User API and display it in list items inside the author’s list. Begin by creating an HTML file and adding a heading and unordered list with the `id` of `authors`:

```html
<h1>Authors</h1>
<ul id="authors"></ul>
```

Now add `script` tags to the bottom of your HTML file and use a DOM selector to grab the `ul`. Use `getElementById` with `authors` as the argument. Remember, `authors` is the `id` for the previously created `ul`:

```html
<script>

    const ul = document.getElementById('authors');

</script>
```

Create a constant variable called `url` which will hold the API URL that will return ten random users:

```javascript
const url = 'https://randomuser.me/api/?results=10';
```

With `ul` and `url` in place, it’s time to create the functions that will be used to create the list items. Create a function called `createNode` that takes a parameter called `element`:

```javascript
function createNode(element) {

}
```

Later, when `createNode` is called, you will need to pass the name of an actual HTML element to create.

Within the function, add a `return` statement that returns `element` using `document.createElement()`:

```javascript
function createNode(element) {
    return document.createElement(element);
}
```

You will also need to create a function called `append` that takes two parameters: `parent` and `el`:

```javascript
function append(parent, el) {

}
```

This function will append `el` to `parent` using `document.createElement`:

```javascript
function append(parent, el) {
    return parent.appendChild(el);
}
```

Both `createNode` and `append` are ready to go. Now using the Fetch API, call the Random User API using `fetch()` with `url` as the argument:

```javascript
fetch(url)
```

```javascript
fetch(url)
  .then(function(data) {

    })
  })
  .catch(function(error) {

  });
```

In the code above, you are calling the Fetch API and passing in the URL to the Random User API. Then a response is received. However, the response you get is not JSON, but an object with a series of methods that can be used depending on what you want to do with the information. To convert the object returned into JSON, use the `json()` method.

Add the `then()` method which will contain a function with a parameter called `resp`:

```javascript
fetch(url)
.then((resp) => )
```

The `resp` parameter takes the value of the object returned from `fetch(url)`. Use the `json()` method to convert `resp` into JSON data:

```javascript
fetch(url)
.then((resp) => resp.json())
```

The JSON data still needs to be processed. Add another `then()` statement with a function that has an argument called `data`:

```javascript
.then(function(data) {

    })
})
```

Within this function, create a variable called `authors` that is set equal to `data.results`:

```javascript
.then(function(data) {
    let authors = data.results;
```

For each author in `authors`, you will want to create a list item that displays a picture of them and displays their name. The `map()` method is great for this:

```javascript
let authors = data.results;
return authors.map(function(author) {

})
```

Within your `map` function, create a variable called `li` that will be set equal to `createNode` with `li` (the HTML element) as the argument:

```javascript
return authors.map(function(author) {
    let li = createNode('li');
})
```

Repeat this to create a `span` element and an `img` element:

```javascript
let li = createNode('li');
let img = createNode('img');
let span = createNode('span');
```

The API offers a name for the author and a picture that goes along with the name. Set the `img.src` to the author picture:

```javascript
let img = createNode('img');
let span = createNode('span');

img.src = author.picture.medium;
```

The `span` element should contain the the first and last name of the `author`. The `innerHTML` property and string interpolation will allow you to do this:

```javascript
img.src = author.picture.medium;
span.innerHTML = `${author.name.first} ${author.name.last}`;
```

With the image and list element created along with the `span` element, you can use the `append` function that was previously created to display these elements on the page:

```javascript
append(li, img);
append(li, span);
append(ul, li);
```

With both `then()` functions completed, you can now add the `catch()` function. This function will log the potential error to the console:

```javascript
.catch(function(error) {
  console.log(error);
});
```

This is the full code of the request you created:

```javascript
function createNode(element) {
    return document.createElement(element);
}

function append(parent, el) {
  return parent.appendChild(el);
}

const ul = document.getElementById('authors');
const url = 'https://randomuser.me/api/?results=10';

fetch(url)
.then((resp) => resp.json())
.then(function(data) {
  let authors = data.results;
  return authors.map(function(author) {
    let li = createNode('li');
    let img = createNode('img');
    let span = createNode('span');
    img.src = author.picture.medium;
    span.innerHTML = `${author.name.first} ${author.name.last}`;
    append(li, img);
    append(li, span);
    append(ul, li);
  })
})
.catch(function(error) {
  console.log(error);
});
```

You just successfully performed a GET request using the Random User API and the Fetch API. In the next step, you will learn how to perform POST requests.

## Step 3 — Handling POST Requests

Fetch defaults to GET requests, but you can use all other types of requests, change the headers, and send data. To do this, you need to set your object and pass it as the second argument of the fetch function.

Before creating a POST request, create the data you would like to send to the API. This will be an object called `data` with the key `name` and value `Sammy` (or your name):

```javascript
const url = 'https://randomuser.me/api';

let data = {
  name: 'Sammy'
}
```

Make sure to include a constant variable that holds the link the Random User API.

Since this is a POST request, you will need to state that explicitly. Create an object called `fetchData`:

```javascript
let fetchData = {

}
```

This object needs to include three keys: `method`, `body`, and `headers`. The `method` key should have the value `'POST'`. `body` should be set equal to the `data` object that was just created. `headers` should have the value of `new Headers()`:

```javascript
let fetchData = {
  method: 'POST',
  body: data,
  headers: new Headers()
}
```

The `Headers` interface is a property of the Fetch API, which allows you to perform various actions on HTTP request and response headers. If you would like to learn more about this, this article called [How To Define Routes and HTTP Request Methods in Express](https://www.digitalocean.com/community/tutorials/nodejs-express-routing) can give you more information.

With this code in place, the POST request can be made using the Fetch API. You will include `url` and `fetchData` as arguments for your `fetch` POST request:

```javascript
fetch(url, fetchData)
```

The `then()` function will include code that handles the response received from the Random User API server:

```javascript
fetch(url, fetchData)
.then(function() {
    // Handle response you get from the server
});
```

To create an object and use the `fetch()` function , there is also another option. Instead of creating an object like `fetchData`, you can use the request constructor to create your request object. To do this, create a variable called `request`:

```javascript
const url = 'https://randomuser.me/api';

let data = {
  name: 'Sara'
}

var request =
```

The `request` variable should be set equal to `new Request`. The `new Request` construct takes two arguments: the API url (`url`) and an object. The object should also include the `method`, `body`, and `headers` keys just like `fetchData`:

```javascript
var request = new Request(url, {
    method: 'POST',
    body: data,
    headers: new Headers()
});
```

Now, `request` can be used as the sole argument for `fetch()` since it also includes the API url:

```javascript
fetch(request)
.then(function() {
    // Handle response we get from the API
})
```

Altogether, your code will look like this:

```javascript
const url = 'https://randomuser.me/api';

let data = {
  name: 'Sara'
}

var request = new Request(url, {
    method: 'POST',
    body: data,
    headers: new Headers()
});

fetch(request)
.then(function() {
    // Handle response we get from the API
})
```

Now you know two methods for creating and executing POST requests with the Fetch API.

## Conclusion

While the Fetch API is not yet supported by all the browsers, it is a great alternative to XMLHttpRequest. If you would like to learn how to call Web APIs using React, [check out this article](https://www.digitalocean.com/community/tutorials/how-to-call-web-apis-with-the-useeffect-hook-in-react) on this very topic.