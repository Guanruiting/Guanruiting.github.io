---
title: How does UmiJS stack up against Next.js?
date: 2021-03-25 11:50:39
tags: 
- React
- Umi
- Nextjs
categories: English
---

![comparing-react-ssr-frameworks-umi-vs-next](https://raw.githubusercontent.com/macshion/PicBed/main/2021/20210325114733.png)

UmiJS is an extensible, enterprise-level React framework authored by [Alipay’s developer team](https://github.com/sorrycc). Alipay uses it in its internal projects, as do several other companies such as [Youku](https://www.youku.com/) and [Netease](https://www.neteasegames.com/).

While exploring this framework, I discovered that it’s similar to Next.js in a handful of interesting ways. Both have support for routing and server-side rendering out of the box as well as TypeScript.

Along the way, I got curious about Umi and decided to look deeper into the framework to see how it compares with Next. I evaluated both frameworks based on the criteria listed below. Here are my findings.

## CSS support

Next has support for [all CSS styling methods](https://nextjs.org/docs/basic-features/built-in-css-support) including CSS in JS, Sass, Stylus, Less, CSS module and Post CSS. You can just import the css file into your pages in case of regular CSS:



```react
// styles.css
body {
  font-family: 'SF Pro Text', 'SF Pro Icons', 'Helvetica Neue', 'Helvetica',
    'Arial', sans-serif;
  padding: 20px 20px 60px;
  max-width: 680px;
  margin: 0 auto;
}

// pages/_app.js
import '../styles.css'

// This default export is required in a new `pages/_app.js` file.
export default function MyApp({ Component, pageProps }) {
  return <Component {...pageProps} />
}
```

Next has official plugins for writing CSS using Sass, Stylus, and Less. If you’re using CSS modules, you’ll need to follow Next’s naming convention, `[name].module.css`.

```react
// Button.module.css
/*
You do not need to worry about .error {} colliding with any other `.css` or
`.module.css` files!
*/
.error {
  color: white;
  background-color: red;
}

// Button.js
import styles from './Button.module.css'

export function Button() {
  return (
    <button
      type="button"
      // Note how the "error" class is accessed as a property on the imported
      // `styles` object.
      className={styles.error}
    >
      Destroy
    </button>
  )
}
```

Umi, on the other hand, has dropped support for Sass and currently supports regular CSS, CSS module, and Less. If you want to use Sass or Stylus, you’ll need to configure the webpack config to do so. Umi automatically recognizes the use of CSS modules.

```javascript
// Example of CSS Modules
import styles from './foo.css';

// Example of Non-CSS Modules
import './foo.css';
```

## webpack customization

Next features such as code splitting, hot code reloading, and server-side rendering already work out of the box. But if you need extra power or just a different configuration, Next allows you to write your own configuration through its [`next.config.js`](https://nextjs.org/docs/api-reference/next.config.js/introduction) module. The config file is a regular Node.js module instead of a JSON file.

```javascript
module.exports = {
  /* config options here */
}
```

Umi also has its [own configuration file](https://umijs.org/docs/config), but it’s in the form of JSON file.

```javascript
export default {
  base: '/docs/',
  publicPath: '/static/',
  hash: true,
  history: {
    type: 'hash',
  },
}
```

## Documentation

I found Next’s documentation to be more detailed in explaining how to use each feature.

To show how each feature works, the docs walk you through building a simple blog app.

![image-20210325142751370](https://raw.githubusercontent.com/macshion/PicBed/main/2021/image-20210325142751370.png)

Another thing to consider: part of Umi’s documentation is not yet translated into English (Umi’s main user base is located in China). I had to use Google Translate feature to help me read the documentation.

![image-20210325142834404](https://raw.githubusercontent.com/macshion/PicBed/main/2021/image-20210325142834404.png)

## CLI support

Umi has some interesting CLI support to generate pages and check the current webpack configuration.

```
Usage: umi <command> [options]

  Commands:

    build     build application for production
    config    umi config cli
    dev       start a dev server for development
    generate  generate code snippets quickly
    help      show command helps
    plugin    inspect umi plugins
    version   show umi version
    webpack   inspect webpack configurations
    dva       
    test      test with jest

  Run `umi help <command>` for more information of specific commands.
  Visit https://umijs.org/ to learn more about Umi.
```

Next’s CLI support is focused solely on helping you to deploy the application.

```
Usage
  $ next <command>

Available commands
  build, start, export, dev, telemetry

Options
  --version, -v   Version number
  --help, -h      Displays this message

For more information run a command with the --help flag
  $ next build --help
```

## Plugin system

Umi’s internal functions are all third-party plugins. The documentation covers how its [plugin system](https://umijs.org/plugins/api) works, complete with a [test framework](https://umijs.org/plugins/test).

Next has its own [set of plugins](https://github.com/vercel/next-plugins), but I can’t seem to find instructions on how to create one and share it with other developers.

## Why Next has the edge

Both Next and Umi fully support building React applications for production with little to no configuration. Next has more complete support for writing CSS and customizing its webpack configuration, while Umi is more opinionated and doesn’t give much support for webpack configurations.

For now, I prefer Next to Umi because I find the Umi documentation a bit hard to understand. I also found more guides for building things with Next, such as e-commerce websites and [static sites](https://scotch.io/@sw-yx/using-nextjs-as-a-static-site-generator-for-netlify).



Original link: [How does UmiJS stack up against Next.js?](https://blog.logrocket.com/comparing-react-ssr-frameworks-umi-vs-next/)