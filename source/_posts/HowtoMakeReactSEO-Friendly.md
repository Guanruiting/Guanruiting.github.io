---
title: 'How to Make React SEO-Friendly: an Extensive SEO Guide'
time: 2020-12-24 16:47:00
tags:
- React
- SEO
- Nextjs
- Gatsby
categories: English
---

React-driven single-page applications (SPAs) are gaining momentum. Used by tech giants like Facebook, Twitter, and Google, React allows for building fast, responsive, and animation-rich websites and web applications with a smooth user experience.

However, products created with React (or any other modern JavaScript framework like Angular, Vue, or Svelte) have limited capabilities for search engine optimization. This becomes a problem if a website mostly acquires customers through website content and[ search marketing](https://blog.hubspot.com/service/customer-acquisition). 

Luckily, there are a couple of ready-made solutions for React that can help you achieve visibility in search engines. We talk about them below. 

But before we dive deep into technical details of optimizing single-page applications (SPA), let’s deal with some useful theory to help you understand the challenges with SEO in React websites.

## What’s a single-page app and why React? 

A single-page application is a web application whose content is served in a single HTML page. This page is dynamically updated, but it doesn’t fully reload each time a user interacts with it. Instead of sending a new request to the server for each interaction and then receiving a whole new page with new content, the client side of a single-page web app only requests and loads data that needs to be updated. 

Facebook, Twitter, Netflix, Trello, Gmail, and Slack are all examples of single-page apps.

From the developer’s perspective, SPAs keep the presentation layer (the front end) and the data layer (the back end) separate, so two teams can develop these parts in parallel. Also, with an SPA, it’s easier to scale and use a microservices architecture than it is with a multi-page app. 

**Read also: [Single-page Apps vs Multi-page Web Apps: What to Choose for Web Development](https://yalantis.com/blog/single-page-apps-vs-multiple-page-apps/)**

From the user’s perspective, single-page apps offer seamless interaction with a web app. Plus, these apps can cache data in local storage, meaning they’ll load even faster the second time. 

When it comes to building an SPA, developers can use one of the popular JavaScript frameworks: React, Angular, or Vue. Among these big three, React holds the top spot. [React ](https://reactjs.org/)is the most popular JavaScript framework according to the 2019 [State of JavaScript](https://2019.stateofjs.com/) Survey.

Thanks to React’s[ component-based](https://reactjs.org/docs/components-and-props.html) architecture, it’s easy to reuse code and divide a large app into smaller parts. Hence, maintaining and debugging large SPA projects is much easier than doing the same for large multi-page apps. The [virtual DOM](https://reactjs.org/docs/faq-internals.html) ensures high app performance. Also, the React library supports all modern browsers, including their older versions. 

**Read also: [7 Best JavaScript Frameworks and Libraries for Frontend Web Development ](https://yalantis.com/blog/javascript-frameworks-how-to-make-your-choice/)**

But as you might have guessed, React has disadvantages as well, and one of the biggest is the lack of SEO-friendliness. 

## Principles of search engine optimization

Search engine optimization (SEO) is the practice of increasing the quality and quantity of web traffic to a website by increasing its visibility on search engines. 

The main task of SEO is to help a web app rank in search engines (Google, Bing) when the target audience searches for information by a certain keyword. Most SEO efforts focus on optimizing apps for Google. After all, as of 2020 Google has a 92.16% search engine market share according to [StatCounter](https://gs.statcounter.com/search-engine-market-share#monthly-202001-202004-bar). 

According to [Backlinko](https://backlinko.com/google-ctr-stats), 75% of all user clicks go to the top three websites in search engine results, while websites from the second results page and beyond get only 0.78% of clicks. That’s why digital businesses are furiously fighting to get on this first page of search results.

For business owners, it’s crucial to think of an SEO optimization strategy from the very beginning of web app development to find an effective technology stack. 

To determine a website’s ranking in search results, search engines use [web crawlers](https://www.google.com/search/howsearchworks/crawling-indexing/). A web crawler is a bot that regularly visits web pages and analyzes them according to specific criteria set by the search engine. Each search engine has its own crawler, and Google’s crawler is called the Googlebot. 

![This is how crawlers work](https://raw.githubusercontent.com/macshion/PicBed/main/images/how-crawlers-work.png)

The Googlebot explores pages link by link, gathers information on website freshness, content uniqueness, number of backlinks, etc., downloads HTML and CSS files, and sends all of this data to Google servers. Then it’s analyzed and indexed by a system called Caffeine. This is a fully automatic process, so it’s vital to ensure that crawlers correctly understand the website content. And here’s where the problem appears. 

## What’s wrong with optimizing single-page applications (SPA) for search engines?

Typically, single-page apps load pages on the client side: at first, the page is an empty container; then JavaScript pushes content to this container. The simplest HTML document for a React app might look as follows:

```javascript
<html lang="en">
<head>
  <title>React App</title>
</head>
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
    <script src="/static/js/bundle.js"></script>
  </body>
</html>
```

As you can see, there’s nothing except the <div> tag and an external script. Single-page applications need a browser to run a script, and only after the script is run will the content be dynamically loaded to the web page. So when a crawler visits the website, it sees an empty page without content. Hence, the page cannot be indexed. 

In autumn 2015, [Google announced](https://webmasters.googleblog.com/2015/10/deprecating-our-ajax-crawling-scheme.html) that their bots would also inspect the JavaScript and CSS of web pages, so they would be able to render and understand web pages like browsers do. That was great news, but there are still problems with SEO optimization:  

- **Long delays**
  

If the content on a page updates frequently, crawlers should regularly revisit the page. This can cause problems, since reindexing may only be done a week later after the content is updated, as Google Chrome developer Paul Kinlan [reports on Twitter](https://mobile.twitter.com/Paul_Kinlan/status/1039852756113080320).

This happens because the Google Web Rendering Service (WRS) enters the game. After a bot has downloaded HTML, CSS, and JavaScript files, the WRS runs the JavaScript code, fetches data from APIs, and only after that sends the data to Google’s servers.

- **Limited crawling budget**
  

The crawl budget is the maximum number of pages on your website that a crawler can process in a certain period of time. Once that time is up, the bot leaves the site no matter how many pages it’s downloaded (whether that’s 26, 3, or 0). If each page takes too long to load because of running scripts, the bot will simply leave your website before indexing it.

Talking about other search engines, Yahoo’s and Bing’s crawlers will still see an empty page instead of dynamically loaded content. So getting your React-based SPA to rank at the top on these search engines is a will-o'-the-wisp.

You should think of how to solve this problem on the stage of designing app architecture.

## Solving the problem

There are a couple of ways to make a React app SEO-friendly: by creating an **isomorphic React** app or by using **prerendering**. 

### Isomorphic React apps

In plain English, an isomorphic JavaScript application (or in our case, an isomorphic React application) can run on both the client side and the server side. 

Thanks to isomorphic JavaScript, you can run the React app and capture the rendered HTML file that’s normally rendered by the browser. This HTML file can then be served to everyone who requests the site (including Googlebot).

On the client side, the app can use this HTML as a base and continue operating on it in the browser as if it had been rendered by the browser. When needed, additional data is added using JavaScript, as an isomorphic app is still dynamic. 

An isomorphic app defines whether the client is able to run scripts or not. When JavaScript is turned off, the code is rendered on the server, so a browser or bot gets all meta tags and content in HTML and CSS. 

When JavaScript is on, only the first page is rendered on the server, so the browser gets HTML, CSS, and JavaScript files. Then JavaScript starts running and the rest of the content is loaded dynamically. Thanks to this, the first screen is displayed faster, the app is compatible with older browsers, and user interactions are smoother in contrast to when websites are rendered on the client side. 

Building an isomorphic app can be really [time-consuming](https://reactjsnews.com/isomorphic-react-in-real-life). Luckily, there are frameworks that facilitate this process. The two most popular solutions for SEO are Next.js and Gatsby.

- [Next.js](https://nextjs.org/) is a framework that helps you create React apps that are generated on the server side quickly and without hassle. It also allows for automatic code splitting and hot code reloading. Next.js can do full-fledged server-side rendering, meaning HTML is generated for each request right when the request is made. 
  
- [Gatsby](https://www.gatsbyjs.org/) is a free open-source compiler that allows developers to make fast and powerful websites. Gatsby doesn’t offer full-fledged server-side rendering. Instead, it generates a static website beforehand and stores generated HTML files in the cloud or on the hosting service. Let’s take a closer look at their approaches. 
  

**Gatsby vs Next.js**

The challenge of SEO for GatsbyJS framework is solved by generating **static websites**. All HTML pages are generated in advance, during the development or build phase, and are then simply loaded to the browser. They contain static data that can be hosted on any hosting service or in the cloud. Such websites are very fast, since they aren’t generated at runtime and don’t wait for data from the database or API. 

But data is only fetched during the build phase. So if your web app has any new content, it won’t be shown until another build is run.

This approach works for apps that don’t update data too frequently, i.e. blogs. But if you want to build a web app that loads hundreds of comments and posts (like forums or social networks), it’s better to opt for another technique. 

The second approach is **server-side rendering (SSR)**, which is offered by Next.js. In contrast with traditional client-side rendering, in server-side rendering, HTML is generated on the server, and then the server sends already generated HTML and CSS files to the browser. Also, with Next.js, HTML is generated each time a client sends a request to the server. This is vital when a web app contains dynamic data (as forums or social networks do). For SSR to work on React, developers also need to use the Node.js server, which can process all requests at runtime. 

**Server-side rendering with Next.js**

The Next.js rendering algorithm looks as follows:

1. The Next.js server, running on Node.js, receives a request and matches it with a certain page (a React component) using a URL address.

2. The page can request data from an API or database, and the server will wait for this data. 

3. The Next.js app generates HTML and CSS based on the received data and existing React components.

4. The server sends a response with HTML, CSS, and JavaScript.

   ![How Next.js works](https://raw.githubusercontent.com/macshion/PicBed/main/images/next-ks.png)

**Making website SEO Friendly with GatsbyJS**

The process of optimizing React applications is divided into two phases: generating a static website during the build and processing requests during runtime.

The [build time process](https://www.gatsbyjs.org/docs/glossary/#build) looks as follows:

1. Gatsby’s bundling tool receives data from an API, CMS, and file system.
   
2. During deployment or setting up a CI/CD pipeline, the tool generates static HTML and CSS on the basis of data and React components.
   
3. After compilation, the tool creates an about folder with an index.html file. The website consists of only static files, which can be hosted on any hosting service or in the cloud.
   

Request processing during runtime happens like this:

1. Gatsby instantly sends HTML, CSS, and JavaScript files to the requested page, since they already were rendered during compilation.
   
2. After JavaScript is loaded to the browser, the website starts working like a typical React app. You can dynamically request data that isn’t important for SEO and work with the website just like you work with a regular single-page React app.

   ![How Gatsby works](https://raw.githubusercontent.com/macshion/PicBed/main/images/gatsby.png)

Creating an isomorphic app is considered the most reliable way to make React SEO-compatible, but it’s not the only option. 

### Prerendering

The idea of prerendering is to preload all HTML elements on the page and cache all SPA pages on the server with the help of [Headless Chrome](https://developers.google.com/web/updates/2017/04/headless-chrome). One popular way to do this is using a prerendering service like [prerender.io](https://prerender.io/). A prerendering service intercepts all requests to your website and, with the help of a user-agent, defines whether a bot or a user is viewing the website.

If the viewer is a bot, it gets the cached HTML version of the page. If it’s a user, the single-page app loads normally. 

![This is how prerendering works](https://raw.githubusercontent.com/macshion/PicBed/main/images/prerendering.png)

Prerendering has a lighter server payload compared to server-side rendering. But on the other hand, most prerendering services are paid and work poorly with dynamically changing content.

## Using Gatsby: A demo project

To demonstrate how isomorphic React apps work, we’ve created a simple [app for the Yalantis blog](http://yalantis-on-gatsby.surge.sh/) using Gatsby. We’ve uploaded the source code of the app to [this repository](https://github.com/ModPhoenix/yalantis-gatsby) on GitHub.

Gatsby renders only the starting page. Then the website works as a single-page app. To see how this isomorphic app works, just turn off JavaScript in your browser’s devtools. If you use Chrome, here are [instructions](https://stackoverflow.com/questions/13405383/how-to-disable-javascript-in-chrome-developer-tools) on how to do that. If you refresh the page, the website should work just like it works with JavaScript turned on.

![Our app with enabled and disabled JavaScript](https://raw.githubusercontent.com/macshion/PicBed/main/images/web-app-with-and-without-js.png)

Now let’s check the audit result using [Lighthouse](https://developers.google.com/web/tools/lighthouse). Its performance is close to 100, while SEO for Gatsby.js applications is measured as high as 90. 

![Lighthouse results](https://raw.githubusercontent.com/macshion/PicBed/main/images/lighthouse.png)

If this website were on the production server, all indicators would be approximately 100. 

## The bottom line 

Single-page React applications offer exceptional performance, seamless interactions close to those of native applications, a lighter server payload, and ease of web development. 

Challenges with SEO shouldn’t be a reason for you to avoid using the React library. Instead, you can use the above-mentioned solutions to fight this issue. Moreover, search engine crawlers are getting smarter every year, so in the future, SEO optimization may no longer be a pitfall of using React.



[https://yalantis.com/blog/search-engine-optimization-for-react-apps/](https://yalantis.com/blog/search-engine-optimization-for-react-apps/)