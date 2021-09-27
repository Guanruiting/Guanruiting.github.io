---
title: Deploy Your Next JS Application in Subfolder
date: 2021-09-27 12:03:07
tags:
- Nextjs
---

You sometimes want to deploy your Next JS under `/blog`, `/docs`, or `/dashboard` folder. But by default, you can only deploy your Next JS on your project root folder.

Since Next JS 9.5, you can change this configuration by setting `basePath` in your `next.config.js`. By default, `basePath` is set to `/` but you can modify to `/blog` or `/docs`:

```js
module.exports = {  basePath: '/docs',};
```

That also means you can also run several Next JS applications under the same domain. You don't need to create a subdomain anymore.

After updating `basePath`, you won't be able to visit `http://localhost:3000` on your local development environment. To continue to browse on your local machine, you need to add `basePath` value after `http://localhost:3000`.

> For your information, you don't need to update your links in your Next JS code. Indeed, it'll automatically prepend `basePath` value to all your links.



Source: https://creativedesignsguru.com/deploy-your-next-js-application-in-subfolder/

