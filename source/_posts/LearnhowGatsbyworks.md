---
title: 'Tutorial: Learn how Gatsby works'
date: 2020-12-25 20:32:00
tags:
- Gatsby
- React
- SSR
categories: English
---

The goal of this tutorial is to guide you through setting up and deploying your first Gatsby site. Along the way, you'll learn some general web development topics as well as the fundamentals of building a Gatsby site.

> **Note:** This tutorial is intended to be as accessible as possible to people without much web development experience. If you prefer to jump straight to code, feel free to skip to [the quick start](https://www.gatsbyjs.com/docs/quick-start).

# Set Up Your Development Environment

Before you start building your first Gatsby site, you’ll need to familiarize yourself with some core web technologies and make sure that you have installed all required software tools.

## Familiarize yourself with the command line

The command line is a text-based interface used to run commands on your computer. You’ll also often see it referred to as the terminal. In this tutorial, we’ll use both interchangeably. It’s a lot like using the Finder on a Mac or Explorer on Windows. Finder and Explorer are examples of graphical user interfaces (GUI). The command line is a powerful, text-based way to interact with your computer.

Take a moment to locate and open up the command line interface (CLI) for your computer. Depending on which operating system you are using, see [**instructions for Mac**](http://www.macworld.co.uk/feature/mac-software/how-use-terminal-on-mac-3608274/), [**instructions for Windows**](https://www.lifewire.com/how-to-open-command-prompt-2618089) or [**instructions for Linux**](https://www.howtogeek.com/140679/beginner-geek-how-to-start-using-the-linux-terminal/).

***Note:** If you’re new to the command line, “running” a command, means “writing a given set of instructions in your command prompt, and hitting the Enter key”. Commands will be shown in a highlighted box, something like `node --version`, but not every highlighted box is a command! If something is a command it will be mentioned as something you have to run/execute.*

## Install Node.js for your appropriate operating system

Node.js is an environment that can run JavaScript code outside of a web browser. Gatsby is built with Node.js. To get up and running with Gatsby, you’ll need to have a recent version installed on your computer. npm comes bundled with Node.js so if you don’t have npm, chances are that you don’t have Node.js either.

### Mac instructions

To install Gatsby and Node.js on a Mac, it is recommended to use [Homebrew](https://brew.sh/). A little set-up in the beginning can save you from some headaches later on!

#### How to install or verify Homebrew on your computer:

1. Open your Terminal.
2. See if Homebrew is installed. You should see “Homebrew” and a version number.

```shell

brew -v
```

1. If not, download and install [Homebrew with the instructions](https://docs.brew.sh/Installation).
2. Once you’ve installed Homebrew, repeat step 2 to verify.

#### Install Xcode Command Line Tools:

1. Open your Terminal.
2. Install Xcode Command line tools by running:

```shell

xcode-select --install
```

> 💡 If that fails, download it [directly from Apple’s site](https://developer.apple.com/download/more/), after signing-in with an Apple developer account.

1. After being prompted to start the installation, you’ll be prompted again to accept a software license for the tools to download.

#### Install Node

1. Open your Terminal
2. Install node with Homebrew:

```shell

brew install node
```

> 💡 If you don’t want to install it through Homebrew, download the latest Node.js version from [the official Node.js website](https://nodejs.org/en/), double click on the downloaded file and go through the installation process.

### Windows Instructions

- Download and install the latest Node.js version from [the official Node.js website](https://nodejs.org/en/)

### Linux Instructions

Install nvm (Node Version Manager) and needed dependencies. nvm is used to manage Node.js and all its associated versions.

> 💡 When installing a package, if it asks for confirmation, type `y` and press enter.

Select your distro:

- [Ubuntu, Debian, and other apt based distros](https://www.gatsbyjs.com/docs/tutorial/part-zero/#ubuntu-debian-and-other-apt-based-distros)
- [Arch, Manjaro and other pacman based distros](https://www.gatsbyjs.com/docs/tutorial/part-zero/#arch-manjaro-and-other-pacman-based-distros)
- [Fedora, RedHat, and other dnf based distros](https://www.gatsbyjs.com/docs/tutorial/part-zero/#fedora-redhat-and-other-dnf-based-distros)

> 💡 If the Linux distribution you are using is not listed here, please find instructions on the web.

#### Ubuntu, Debian, and other `apt` based distros:

1. Make sure your Linux distribution is ready to go run an update and an upgrade:

```shell

sudo apt update
sudo apt -y upgrade
```

1. Install curl which allows you to transfer data and download additional dependencies:

```shell

sudo apt-get install curl
```

1. After it finishes installing, download the latest nvm version:

```shell

curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
```

1. Confirm this has worked. The output should be a version number.

```shell

nvm --version
```

1. Continue with the section: [Set default Node.js version](https://www.gatsbyjs.com/docs/tutorial/part-zero/#set-default-nodejs-version)

#### Arch, Manjaro and other `pacman` based distros:

1. Make sure your distribution is ready to go:

```shell

sudo pacman -Syu
```

1. These distros come installed with curl, so you can use that to download nvm:

```shell

curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
```

1. Before using nvm, you need to install additional dependencies by running:

```shell

sudo pacman -S grep awk tar
```

1. Confirm this has worked. The output should be a version number.

```shell

nvm --version
```

1. Continue with the section: [Set default Node.js version](https://www.gatsbyjs.com/docs/tutorial/part-zero/#set-default-nodejs-version)

#### Fedora, RedHat, and other `dnf` based distros:

1. These distros come installed with curl, so you can use that to download nvm:

```shell

curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
```

1. Confirm this has worked. The output should be a version number.

```shell

nvm --version
```

1. Continue with the section: [Set default Node.js version](https://www.gatsbyjs.com/docs/tutorial/part-zero/#set-default-nodejs-version)

#### Set default Node.js version

When nvm is installed, it does not default to a particular node version. You’ll need to install the version you want and give nvm instructions to use it. This example uses the version 10 release, but more recent version numbers can be used instead.

```shell

nvm install 10
nvm use 10
```

Confirm that this worked:

```shell

npm --version
node --version
```

The output should look similar to the screenshot below, showing version numbers in response to the commands.

![img](https://www.gatsbyjs.com/static/71e043f06cc476acc6722818e647e517/f8915/01-node-npm-versions.png)

Once you have followed the installation steps and you have checked everything is installed properly, you can continue to the next step.

## Install Git

Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency. When you install a Gatsby “starter” site, Gatsby uses Git behind the scenes to download and install the required files for your starter. You will need to have Git installed to set up your first Gatsby site.

The steps to download and install Git depend on your operating system. Follow the guide for your system:

- [Install Git on macOS](https://www.atlassian.com/git/tutorials/install-git#mac-os-x)
- [Install Git on Windows](https://www.atlassian.com/git/tutorials/install-git#windows)
- [Install Git on Linux](https://www.atlassian.com/git/tutorials/install-git#linux)

## Using the Gatsby CLI

The Gatsby CLI tool lets you quickly create new Gatsby-powered sites and run commands for developing Gatsby sites. It is a published npm package.

The Gatsby CLI is available via npm and should be installed globally by running:

```shell

npm install -g gatsby-cli
```

***Note**: when you install Gatsby and run it for the first time, you’ll see a short message notifying you about anonymous usage data that is being collected for Gatsby commands, you can read more about how that data is pulled out and used in the [telemetry doc](https://www.gatsbyjs.com/docs/telemetry).*

See the available commands:

```shell

gatsby --help
```

[![Check gatsby commands in terminal](https://www.gatsbyjs.com/static/fac15c37d0c4e262ae8a3e4dcdf9251f/748f4/05-gatsby-help.png)](https://www.gatsbyjs.com/static/fac15c37d0c4e262ae8a3e4dcdf9251f/748f4/05-gatsby-help.png)

> 💡 If you are unable to successfully run the Gatsby CLI due to a permissions issue, you may want to check out the [npm docs on fixing permissions](https://docs.npmjs.com/getting-started/fixing-npm-permissions), or [this guide](https://github.com/sindresorhus/guides/blob/master/npm-global-without-sudo.md).

## Create a Gatsby site

Now you are ready to use the Gatsby CLI tool to create your first Gatsby site. Using the tool, you can download “starters” (partially built sites with some default configuration) to help you get moving faster on creating a certain type of site. The “Hello World” starter you’ll be using here is a starter with the bare essentials needed for a Gatsby site.

1. Open up your terminal.
2. Create a new site from a starter:

```shell

gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world
```

> 💡 What happened?
>
> - `new` is a gatsby command to create a new Gatsby project.
> - Here, `hello-world` is an arbitrary title — you could pick anything. The CLI tool will place the code for your new site in a new folder called “hello-world”.
> - Lastly, the GitHub URL specified points to a code repository that holds the starter code you want to use.

> 💡 Depending on your download speed, the amount of time this takes will vary. For brevity’s sake, the gif below was paused during part of the install

1. Change into the working directory:

```shell

cd hello-world
```

> 💡 This says *‘I want to change directories (`cd`) to the “hello-world” subfolder’*. Whenever you want to run any commands for your site, you need to be in the context for that site (aka, your terminal needs to be pointed at the directory where your site code lives).

1. Start the development mode:

```shell

gatsby develop
```

> 💡 This command starts a development server. You will be able to see and interact with your new site in a development environment — local (on your computer, not published to the internet).

<video controls="" autoplay="" loop="" style="box-sizing: inherit; display: inline-block; width: 702px; margin-bottom: 1.5rem;"></video>

### View your site locally

Open up a new tab in your browser and navigate to `http://localhost:8000/`

[![Check homepage](https://www.gatsbyjs.com/static/057f454229859b1752c44dba1580984e/321ea/04-home-page.png)](https://www.gatsbyjs.com/static/057f454229859b1752c44dba1580984e/a8c87/04-home-page.png)

Congrats! This is the beginning of your very first Gatsby site! 🎉

You’ll be able to visit the site locally at `http://localhost:8000/` for as long as your development server is running. That’s the process you started by running the `gatsby develop` command. To stop running that process (or to “stop running the development server”), go back to your terminal window, hold down the “control” key, and then hit “c” (ctrl-c). To start it again, run `gatsby develop` again!

***Note:** If you are using VM setup like `vagrant` and/or would like to listen on your local IP address, run `gatsby develop --host=0.0.0.0`. Now, the development server listens on both `http://localhost` and your local IP.*

## Set up a code editor

A code editor is a program designed specifically for editing computer code. There are many great ones out there.

### Download VS Code

Gatsby documentation sometimes includes screenshots that were taken in VS Code, so if you don’t have a preferred code editor yet, using VS Code will make sure that your screen looks like the screenshots in the tutorial and docs. If you choose to use VS Code, visit the [VS Code site](https://code.visualstudio.com/#alt-downloads) and download the version appropriate for your platform.

### Install the Prettier plugin

We also recommend using [Prettier](https://github.com/prettier/prettier), a tool that helps format your code to avoid errors.

You can use Prettier directly in your editor using the [Prettier VS Code plugin](https://github.com/prettier/prettier-vscode):

1. Open the extensions view on VS Code (View => Extensions).
2. Search for “Prettier - Code formatter”.
3. Click “Install”. (After installation, you’ll be prompted to restart VS Code to enable the extension. Newer versions of VS Code will automatically enable the extension after download.)

> 💡 If you’re not using VS Code, check out the Prettier docs for [install instructions](https://prettier.io/docs/en/install.html) or [other editor integrations](https://prettier.io/docs/en/editors.html).

## ➡️ What’s Next?

To summarize, in this section you:

- Learned about the command line and how to use it
- Installed and learned about Node.js and the npm CLI tool, the version control system Git, and the Gatsby CLI tool
- Generated a new Gatsby site using the Gatsby CLI tool
- Ran the Gatsby development server and visited your site locally
- Downloaded a code editor
- Installed a code formatter called Prettier

Now, move on to [**getting to know Gatsby building blocks**](https://www.gatsbyjs.com/docs/tutorial/part-one/).

## References

### Overview of core technologies

It’s not necessary to be an expert with these already — if you’re not, don’t worry! You’ll pick up a lot through the course of this tutorial series. These are some of the main web technologies you’ll use when building a Gatsby site:

- **HTML**: A markup language that every web browser is able to understand. It stands for HyperText Markup Language. HTML gives your web content a universal informational structure, defining things like headings, paragraphs, and more.
- **CSS**: A presentational language used to style the appearance of your web content (fonts, colors, layout, etc). It stands for Cascading Style Sheets.
- **JavaScript**: A programming language that helps us make the web dynamic and interactive.
- **React**: A code library (built with JavaScript) for building user interfaces. It’s the framework that Gatsby uses to build pages and structure content.
- **GraphQL**: A query language that allows you to pull data into your website. It’s the interface that Gatsby uses for managing site data.

### What is a website?

For a comprehensive introduction to what a website is — including an intro to HTML and CSS — check out “[**Building your first web page**](https://learn.shayhowe.com/html-css/building-your-first-web-page/)”. It’s a great place to start learning about the web. For a more hands-on introduction to [**HTML**](https://www.codecademy.com/learn/learn-html), [**CSS**](https://www.codecademy.com/learn/learn-css), and [**JavaScript**](https://www.codecademy.com/learn/introduction-to-javascript), check out the tutorials from Codecademy. [**React**](https://reactjs.org/tutorial/tutorial.html) and [**GraphQL**](https://graphql.org/graphql-js/) also have their own introductory tutorials.

### Learn more about the command line

For a great introduction to using the command line, check out [**Codecademy’s Command Line tutorial**](https://www.codecademy.com/courses/learn-the-command-line/lessons/navigation/exercises/your-first-command) for Mac and Linux users, and [**this tutorial**](https://www.computerhope.com/issues/chusedos.htm) for Windows users. Even if you are a Windows user, the first page of the Codecademy tutorial is a valuable read. It explains what the command line is, not how to interface with it.

### Learn more about npm

npm is a JavaScript package manager. A package is a module of code that you can choose to include in your projects. If you downloaded and installed Node.js, npm was installed with it!

npm has three distinct components: the npm website, the npm registry, and the npm command line interface (CLI).

- On the npm website, you can browse what JavaScript packages are available in the npm registry.
- The npm registry is a large database of information about JavaScript packages available on npm.
- Once you’ve identified a package you want, you can use the npm CLI to install it in your project or globally (like other CLI tools). The npm CLI is what talks to the registry — you generally only interact with the npm website or the npm CLI.

> 💡 Check out npm’s introduction, “[**What is npm?**](https://docs.npmjs.com/getting-started/what-is-npm)”.

### Learn more about Git

You will not need to know Git to complete this tutorial, but it is a very useful tool. If you are interested in learning more about version control, Git, and GitHub, check out GitHub’s [Git Handbook](https://guides.github.com/introduction/git-handbook/).



# Get to Know Gatsby Building Blocks

In the [**previous section**](https://www.gatsbyjs.com/docs/tutorial/part-zero/), you prepared your local development environment by installing the necessary software and creating your first Gatsby site using the [**“hello world” starter**](https://github.com/gatsbyjs/gatsby-starter-hello-world). Now, take a deeper dive into the code generated by that starter.

## Using Gatsby starters

In [**tutorial part zero**](https://www.gatsbyjs.com/docs/tutorial/part-zero/), you created a new site based on the “hello world” starter using the following command:

```shell

gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world
```

When creating a new Gatsby site, you can use the following command structure to create a new site based on any existing Gatsby starter:

```shell

gatsby new [SITE_DIRECTORY_NAME] [URL_OF_STARTER_GITHUB_REPO]
```

If you omit a URL from the end, Gatsby will automatically generate a site for you based on the [**default starter**](https://github.com/gatsbyjs/gatsby-starter-default). For this section of the tutorial, stick with the “Hello World” site you already created in tutorial part zero. You can learn more about [modifying starters](https://www.gatsbyjs.com/docs/modifying-a-starter) in the docs.

### ✋ Open up the code

In your code editor, open up the code generated for your “Hello World” site and take a look at the different directories and files contained in the ‘hello-world’ directory. It should look something like this:

[![Hello World project in VS Code](https://www.gatsbyjs.com/static/6fd22a2eaed057cc2692ac3a86404864/cab8c/01-hello-world-vscode.png)](https://www.gatsbyjs.com/static/6fd22a2eaed057cc2692ac3a86404864/cab8c/01-hello-world-vscode.png)

*Note: Again, the editor shown here is Visual Studio Code. If you’re using a different editor, it will look a little different.*

Let’s take a look at the code that powers the homepage.

> 💡 If you stopped your development server after running `gatsby develop` in the previous section, start it up again now — time to make some changes to the hello-world site!

## Familiarizing with Gatsby pages

Open up the `/src` directory in your code editor. Inside is a single directory: `/pages`.

Open the file at `src/pages/index.js`. The code in this file creates a component that contains a single div and some text — appropriately, “Hello world!”

### ✋ Make changes to the “Hello World” homepage

1. Change the “Hello World!” text to “Hello Gatsby!” and save the file. If your windows are side-by-side, you can see that your code and content changes are reflected almost instantly in the browser after you save the file.

<video controls="" autoplay="" loop="" style="box-sizing: inherit; display: inline-block; width: 702px; margin-bottom: 1.5rem;"></video>

> 💡 Gatsby uses **hot reloading** to speed up your development process. Essentially, when you’re running a Gatsby development server, the Gatsby site files are being “watched” in the background — any time you save a file, your changes will be immediately reflected in the browser. You don’t need to hard refresh the page or restart the development server — your changes just appear.

1. Now you can make your changes a little more visible. Try replacing the code in `src/pages/index.js` with the code below and save again. You’ll see changes to the text — the text color will be purple and the font size will be larger.

src/pages/index.js

```jsx
Copysrc/pages/index.js: copy code to clipboard
import React from "react"

export default function Home() {
  return <div style={{ color: `purple`, fontSize: `72px` }}>Hello Gatsby!</div>
}
```

> 💡 We’ll be covering more about styling in Gatsby in [**part two**](https://www.gatsbyjs.com/docs/tutorial/part-two/) of the tutorial.

1. Remove the font size styling, change the “Hello Gatsby!” text to a level-one header, and add a paragraph beneath the header.

src/pages/index.js

```jsx
Copysrc/pages/index.js: copy code to clipboard
import React from "react"

export default function Home() {
  return (
    <div style={{ color: `purple` }}>
      <h1>Hello Gatsby!</h1>
      <p>What a world.</p>
    </div>
  );
}
```

[![More changes with hot reloading](https://www.gatsbyjs.com/static/738f82e862eca8d878d19de628291f67/321ea/03-more-hot-reloading.png)](https://www.gatsbyjs.com/static/738f82e862eca8d878d19de628291f67/6fcb6/03-more-hot-reloading.png)

1. Add an image. (In this case, a random image from Unsplash).

src/pages/index.js

```jsx
Copysrc/pages/index.js: copy code to clipboard
import React from "react"

export default function Home() {
  return (
    <div style={{ color: `purple` }}>
      <h1>Hello Gatsby!</h1>
      <p>What a world.</p>
      <img src="https://source.unsplash.com/random/400x200" alt="" />
    </div>
  )
}
```

[![Add image](https://www.gatsbyjs.com/static/ae64a18bc63a9713d0a88f2570abe0dc/321ea/04-add-image.png)](https://www.gatsbyjs.com/static/ae64a18bc63a9713d0a88f2570abe0dc/891d5/04-add-image.png)

### Wait… HTML in our JavaScript?

*If you’re familiar with React and JSX, feel free to skip this section.* If you haven’t worked with the React framework before, you may be wondering what HTML is doing in a JavaScript function. Or why we’re importing `react` on the first line but seemingly not using it anywhere. This hybrid “HTML-in-JS” is actually a syntax extension of JavaScript, for React, called JSX. You can follow along with this tutorial without prior experience with React, but if you’re curious, here’s a brief primer…

Consider the original contents of the `src/pages/index.js` file:

src/pages/index.js

```jsx
Copysrc/pages/index.js: copy code to clipboard
import React from "react"

export default function Home() {
  return <div>Hello world!</div>
}
```

In pure JavaScript, it looks more like this:

src/pages/index.js

```javascript
Copysrc/pages/index.js: copy code to clipboard
import React from "react"

export default function Home() {
  return React.createElement("div", null, "Hello world!")
}
```

Now you can spot the use of the `'react'` import! But wait. You’re writing JSX, not pure HTML and JavaScript. How does the browser read that? The short answer: It doesn’t. Gatsby sites come with tooling already set up to convert your source code into something that browsers can interpret.

## Building with components

The homepage you were just making edits to was created by defining a page component. What exactly is a “component”?

Broadly defined, a component is a building block for your site; It is a self-contained piece of code that describes a section of UI (user interface).

Gatsby is built on React. When we talk about using and defining **components**, we are really talking about **React components** — self-contained pieces of code (usually written with JSX) that can accept input and return React elements describing a section of UI.

One of the big mental shifts you make when starting to build with components (if you are already a developer) is that now your CSS, HTML, and JavaScript are tightly coupled and often living even within the same file.

While a seemingly simple change, this has profound implications for how you think about building websites.

Take the example of creating a custom button. In the past, you would create a CSS class (perhaps `.primary-button`) with your custom styles and then use it whenever you want to apply those styles. For example:

```html

<button class="primary-button">Click me</button>
```

In the world of components, you instead create a `PrimaryButton` component with your button styles and use it throughout your site like:

```jsx

<PrimaryButton>Click me</PrimaryButton>
```

Components become the base building blocks of your site. Instead of being limited to the building blocks the browser provides, e.g. `<button />`, you can easily create new building blocks that elegantly meet the needs of your projects.

### ✋ Using page components

Any React component defined in `src/pages/*.js` will automatically become a page. Let’s see this in action.

You already have a `src/pages/index.js` file that came with the “Hello World” starter. Let’s create an about page.

1. Create a new file at `src/pages/about.js`, copy the following code into the new file, and save.

src/pages/about.js

```jsx
Copysrc/pages/about.js: copy code to clipboard
import React from "react"

export default function About() {
  return (
    <div style={{ color: `teal` }}>
      <h1>About Gatsby</h1>
      <p>Such wow. Very React.</p>
    </div>
  )
}
```

1. Navigate to `http://localhost:8000/about/`

[![New about page](https://www.gatsbyjs.com/static/ff70fd3cbfd3a0e931b899ca245322fc/f1d1f/05-about-page.png)](https://www.gatsbyjs.com/static/ff70fd3cbfd3a0e931b899ca245322fc/f1d1f/05-about-page.png)

Just by putting a React component in the `src/pages/about.js` file, you now have a page accessible at `/about`.

### ✋ Using sub-components

Let’s say the homepage and the about page both got quite large and you were rewriting a lot of things. You can use sub-components to break the UI into reusable pieces. Both of your pages have `<h1>` headers — create a component that will describe a `Header`.

1. Create a new directory at `src/components` and a file within that directory called `header.js`.
2. Add the following code to the new `src/components/header.js` file.

src/components/header.js

```jsx
Copysrc/components/header.js: copy code to clipboard
import React from "react"

export default function Header() {
  return <h1>This is a header.</h1>
}
```

1. Modify the `about.js` file to import the `Header` component. Replace the `h1` markup with `<Header />`:

src/pages/about.js

```jsx
Copysrc/pages/about.js: copy code to clipboard
import React from "react"
import Header from "../components/header"

export default function About() {
  return (
    <div style={{ color: `teal` }}>
      <Header />
      <p>Such wow. Very React.</p>
    </div>
  )
}
```

[![Adding Header component](https://www.gatsbyjs.com/static/ff64a1f15ebbe5e1f1aad740d0686ff7/321ea/06-header-component.png)](https://www.gatsbyjs.com/static/ff64a1f15ebbe5e1f1aad740d0686ff7/fb4e7/06-header-component.png)

In the browser, the “About Gatsby” header text should now be replaced with “This is a header.” But you don’t want the “About” page to say “This is a header.” You want it to say, “About Gatsby”.

1. Head back to `src/components/header.js` and make the following change:

src/components/header.js

```jsx
Copysrc/components/header.js: copy code to clipboard
import React from "react"

export default function Header(props) {
  return <h1>{props.headerText}</h1>
}
```

1. Head back to `src/pages/about.js` and make the following change:

src/pages/about.js

```jsx
Copysrc/pages/about.js: copy code to clipboard
import React from "react"
import Header from "../components/header"

export default function About() {
  return (
    <div style={{ color: `teal` }}>
      <Header headerText="About Gatsby" />
      <p>Such wow. Very React.</p>
    </div>
  )
}
```

[![Passing data to header](https://www.gatsbyjs.com/static/a7da09d0252e86518be87c3608bb1c85/321ea/07-pass-data-header.png)](https://www.gatsbyjs.com/static/a7da09d0252e86518be87c3608bb1c85/f2b95/07-pass-data-header.png)

You should now see your “About Gatsby” header text again!

### What are “props”?

Earlier, you defined React components as reusable pieces of code describing a UI. To make these reusable pieces dynamic you need to be able to supply them with different data. You do that with input called “props”. Props are (appropriately enough) properties supplied to React components.

In `about.js` you passed a `headerText` prop with the value of `"About Gatsby"` to the imported `Header` sub-component:

src/pages/about.js

```jsx
Copysrc/pages/about.js: copy code to clipboard
<Header headerText="About Gatsby" />
```

Over in `header.js`, the header component expects to receive the `headerText` prop (because you’ve written it to expect that). So you can access it like so:

src/components/header.js

```jsx
Copysrc/components/header.js: copy code to clipboard
<h1>{props.headerText}</h1>
```

> 💡 In JSX, you can embed any JavaScript expression by wrapping it with `{}`. This is how you can access the `headerText` property (or “prop!”) from the “props” object.

If you had passed another prop to your `<Header />` component, like so…

src/pages/about.js

```jsx
Copysrc/pages/about.js: copy code to clipboard
<Header headerText="About Gatsby" arbitraryPhrase="is arbitrary" />
```

…you would have been able to also access the `arbitraryPhrase` prop: `{props.arbitraryPhrase}`.

1. To emphasize how this makes your components reusable, add an extra `<Header />` component to the about page, add the following code to the `src/pages/about.js` file, and save.

src/pages/about.js

```jsx
Copysrc/pages/about.js: copy code to clipboard
import React from "react"
import Header from "../components/header"

export default function About() {
  return (
    <div style={{ color: `teal` }}>
      <Header headerText="About Gatsby" />
      <Header headerText="It's pretty cool" />
      <p>Such wow. Very React.</p>
    </div>
  )
}
```

[![Duplicate header to show reusability](https://www.gatsbyjs.com/static/439851d3a4ba8a727b4c07abefce54a9/321ea/08-duplicate-header.png)](https://www.gatsbyjs.com/static/439851d3a4ba8a727b4c07abefce54a9/891d5/08-duplicate-header.png)

And there you have it; A second header — without rewriting any code — by passing different data using props.

### Using layout components

Layout components are for sections of a site that you want to share across multiple pages. For example, Gatsby sites will commonly have a layout component with a shared header and footer. Other common things to add to layouts include a sidebar and/or a navigation menu.

You’ll explore layout components in [**part three**](https://www.gatsbyjs.com/docs/tutorial/part-three/).

## Linking between pages

You’ll often want to link between pages — Let’s look at routing in a Gatsby site.

### ✋ Using the `<Link />` component

1. Open the index page component (`src/pages/index.js`), import the `<Link />` component from Gatsby, add a `<Link />` component above the header, and give it a `to` property with the value of `"/contact/"` for the pathname:

src/pages/index.js

```jsx
Copysrc/pages/index.js: copy code to clipboard
import React from "react"
import { Link } from "gatsby"
import Header from "../components/header"

export default function Home() {
  return (
    <div style={{ color: `purple` }}>
      <Link to="/contact/">Contact</Link>
      <Header headerText="Hello Gatsby!" />
      <p>What a world.</p>
      <img src="https://source.unsplash.com/random/400x200" alt="" />
    </div>
  )
}
```

When you click the new “Contact” link on the homepage, you should see…

[![Gatsby dev 404 page](https://www.gatsbyjs.com/static/5b621cd422b1ccc1181808580a57dd32/6bbf7/09-dev-404.png)](https://www.gatsbyjs.com/static/5b621cd422b1ccc1181808580a57dd32/6bbf7/09-dev-404.png)

…the Gatsby development 404 page. Why? Because you’re attempting to link to a page that doesn’t exist yet.

1. Now you’ll have to create a page component for your new “Contact” page at `src/pages/contact.js` and have it link back to the homepage:

src/pages/contact.js

```jsx
Copysrc/pages/contact.js: copy code to clipboard
import React from "react"
import { Link } from "gatsby"
import Header from "../components/header"

export default function Contact() {
  return (
    <div style={{ color: `teal` }}>
      <Link to="/">Home</Link>
      <Header headerText="Contact" />
      <p>Send us a message!</p>
    </div>
  )
}
```

After you save the file, you should see the contact page and be able to follow the link to the homepage.

<video controls="" loop="" style="box-sizing: inherit; display: inline-block; width: 702px; margin-bottom: 1.5rem;"></video>

The Gatsby `<Link />` component is for linking between pages within your site. For external links to pages not handled by your Gatsby site, use the regular HTML `<a>` tag.

## Deploying a Gatsby site

Gatsby is a *modern site generator*, which means there are no servers to set up or complicated databases to deploy. Instead, the Gatsby `build` command produces a directory of static HTML and JavaScript files which you can deploy to a static site hosting service.

Try using [Surge](https://surge.sh/) for deploying your first Gatsby website. Surge is one of many “static site hosts” which makes it possible to deploy Gatsby sites.

> Gatsby Cloud is another deployment option, built by the team behind Gatsby. In the next section, you’ll find instructions for [deploying to Gatsby Cloud](https://www.gatsbyjs.com/docs/tutorial/part-one/#alternative-deploying-to-gatsby-cloud).

If you haven’t previously installed & set up Surge, open a new terminal window and install their command-line tool:

```shell

npm install --global surge

# Then create a (free) account with them
surge login
```

Next, build your site by running the following command in the terminal at the root of your site (tip: make sure you’re running this command at the root of your site, in this case in the hello-world folder, which you can do by opening a new tab in the same window you used to run `gatsby develop`):

```shell

gatsby build
```

The build should take 15-30 seconds. Once the build is finished, it’s interesting to take a look at the files that the `gatsby build` command just prepared to deploy.

Take a look at a list of the generated files by typing in the following terminal command into the root of your site, which will let you look at the `public` directory:

```shell

ls public
```

Then finally deploy your site by publishing the generated files to surge.sh. For newly-created surge account, you need to verify your email with surge before publishing your site (check your inbox first and verify your email).

```shell

surge public/
```

> Note that you will have to press the `enter` key after you see the `domain: some-name.surge.sh` information on your command-line interface.

Once this finishes running, you should see in your terminal something like:

[![Screenshot of publishing Gatsby site with Surge](https://www.gatsbyjs.com/static/2718feec8167496f9e7a5087a5f539e7/321ea/surge-deployment.png)](https://www.gatsbyjs.com/static/2718feec8167496f9e7a5087a5f539e7/f32b7/surge-deployment.png)

Open the web address listed on the bottom line (`lowly-pain.surge.sh` in this case) and you’ll see your newly published site! Great work!

### Alternative: Deploying to Gatsby Cloud

[Gatsby Cloud](https://gatsbyjs.com/) is a platform built specifically for Gatsby sites, with features like real-time previews, fast builds, and integrations with dozens of other tools. It’s the best place to build and deploy sites built with Gatsby, and you can use Gatsby Cloud free for personal projects.

To deploy your site to Gatsby Cloud, create an account on [GitHub](https://github.com/) if you don’t have one. GitHub allows you to host and collaborate on code projects using Git for version control.

Create a new repository on GitHub. Since you’re importing your existing project, you’ll want a completely empty one, so don’t initialize it with `README` or `.gitignore` files.

You can tell Git where the remote (i.e. not on your computer) repository is like this:

```shell

git remote add origin [GITHUB_REPOSITORY_URL]
```

When you created a new Gatsby project with a starter, it automatically made an initial `git commit`, or a set of changes. Now, you can push your changes to the new remote location:

```shell

git push -u origin master
```

Now you’re ready to link this GitHub repository right to Gatsby Cloud! Check out the reference guide on [Deploying to Gatsby Cloud](https://www.gatsbyjs.com/docs/how-to/previews-deploys-hosting/deploying-to-gatsby-cloud/#set-up-an-existing-gatsby-site).

## ➡️ What’s Next?

In this section you:

- Learned about Gatsby starters, and how to use them to create new projects
- Learned about JSX syntax
- Learned about components
- Learned about Gatsby page components and sub-components
- Learned about React “props” and reusing React components

Now, move on to [**adding styles to your site**](https://www.gatsbyjs.com/docs/tutorial/part-two/)!



# Introduction to Styling in Gatsby

Welcome to part two of the Gatsby tutorial!

## What’s in this tutorial?

In this part, you’re going to explore options for styling Gatsby websites and dive deeper into using React components for building sites.

## Using global styles

Every site has some sort of global style. This includes things like the site’s typography and background colors. These styles set the overall feel of the site — much like the color and texture of a wall sets the overall feel of a room.

### Creating global styles with standard CSS files

One of the most straightforward ways to add global styles to a site is using a global `.css` stylesheet.

#### ✋ Create a new Gatsby site

Start by creating a new Gatsby site. It may be best (especially if you’re new to the command line) to close the terminal windows you used for [part one](https://www.gatsbyjs.com/docs/tutorial/part-one/) and start a new terminal session for part two.

Open a new terminal window, create a new “hello world” Gatsby site in a directory called `tutorial-part-two`, and then move to this new directory:

```shell

gatsby new tutorial-part-two https://github.com/gatsbyjs/gatsby-starter-hello-world
cd tutorial-part-two
```

You now have a new Gatsby site (based on the Gatsby “hello world” starter) with the following structure:

```text

├── package.json
├── src
│   └── pages
│       └── index.js
```

#### ✋ Add styles to a CSS file

1. Create a `.css` file in your new project:

```shell

cd src
mkdir styles
cd styles
touch global.css
```

> Note: Feel free to create these directories and files using your code editor, if you’d prefer.

You should now have a structure like this:

```text

├── package.json
├── src
│   └── pages
│       └── index.js
│   └── styles
│       └── global.css
```

1. Define some styles in the `global.css` file:

src/styles/global.css

```css
Copysrc/styles/global.css: copy code to clipboard
html {
  background-color: lavenderblush;
}
```

> Note: The placement of the example CSS file in a `/src/styles/` folder is arbitrary.

#### ✋ Include the stylesheet in `gatsby-browser.js`

1. Create the `gatsby-browser.js`

```shell

cd ../..
touch gatsby-browser.js
```

Your project’s file structure should now look like this:

```text

├── package.json
├── src
│   └── pages
│       └── index.js
│   └── styles
│       └── global.css
├── gatsby-browser.js
```

> 💡 What is `gatsby-browser.js`? Don’t worry about this too much and for now, just know that `gatsby-browser.js` is one of a handful of special files that Gatsby looks for and uses (if they exist). Here, the naming of the file **is** important. If you do want to explore more now, check out [the docs](https://www.gatsbyjs.com/docs/reference/config-files/gatsby-browser/).

1. Import your recently-created stylesheet in the `gatsby-browser.js` file:

gatsby-browser.js

```javascript
Copygatsby-browser.js: copy code to clipboard
import "./src/styles/global.css"

// or:
// require('./src/styles/global.css')
```

> Note: Both CommonJS (`require`) and ES Module (`import`) syntax work here. If you’re not sure which to choose, `import` is usually a good default. When working with files that are only run in a Node.js environment however (like `gatsby-node.js`), `require` will need to be used.

1. Start the development server:

```shell

gatsby develop
```

If you take a look at your project in the browser, you should see a lavender background applied to the “hello world” starter:

[![Lavender Hello World!](https://www.gatsbyjs.com/static/4ddb5fc342a06be749f8a14b86b1edc2/321ea/global-css.png)](https://www.gatsbyjs.com/static/4ddb5fc342a06be749f8a14b86b1edc2/6f278/global-css.png)

> Tip: This part of the tutorial has focused on the quickest and most straightforward way to get started styling a Gatsby site — importing standard CSS files directly, using `gatsby-browser.js`. In most cases, the best way to add global styles is with a shared layout component. [Check out the docs](https://www.gatsbyjs.com/docs/how-to/styling/global-css/) for more on that approach.

## Using component-scoped CSS

So far, we’ve talked about the more traditional approach of using standard CSS stylesheets. Now, we’ll talk about various methods of modularizing CSS to tackle styling in a component-oriented way.

### CSS Modules

Let’s explore **CSS Modules**. Quoting from [the CSS Module homepage](https://github.com/css-modules/css-modules):

> A **CSS Module** is a CSS file in which all class names and animation names are scoped locally by default.

CSS Modules are very popular because they let you write CSS normally but with a lot more safety. The tool automatically generates unique class and animation names, so you don’t have to worry about selector name collisions.

Gatsby works out of the box with CSS Modules. This approach is highly recommended for those new to building with Gatsby (and React in general).

#### ✋ Build a new page using CSS Modules

In this section, you’ll create a new page component and style that page component using a CSS Module.

First, create a new `Container` component.

1. Create a new directory at `src/components` and then, in this new directory, create a file named `container.js` and paste the following:

src/components/container.js

```jsx
Copysrc/components/container.js: copy code to clipboard
import React from "react"
import containerStyles from "./container.module.css"

export default function Container({ children }) {
  return <div className={containerStyles.container}>{children}</div>
}
```

You’ll notice you imported a CSS module file named `container.module.css`. Let’s create that file now.

1. In the same directory (`src/components`), create a `container.module.css` file and copy/paste the following:

src/components/container.module.css

```css
Copysrc/components/container.module.css: copy code to clipboard
.container {
  margin: 3rem auto;
  max-width: 600px;
}
```

You’ll notice that the file name ends with `.module.css` instead of the usual `.css`. This is how you tell Gatsby that this CSS file should be processed as a CSS module rather than plain CSS.

1. Create a new page component by creating a file at `src/pages/about-css-modules.js`:

src/pages/about-css-modules.js

```jsx
Copysrc/pages/about-css-modules.js: copy code to clipboard
import React from "react"

import Container from "../components/container"

export default function About() {
  return (
    <Container>
      <h1>About CSS Modules</h1>
      <p>CSS Modules are cool</p>
    </Container>
  )
}
```

Now, if you visit `http://localhost:8000/about-css-modules/`, your page should look something like this:

[![Page with CSS module styles](https://www.gatsbyjs.com/static/e5678fdf693c054d7f09cbc69be85567/321ea/css-modules-basic.png)](https://www.gatsbyjs.com/static/e5678fdf693c054d7f09cbc69be85567/0f586/css-modules-basic.png)

#### ✋ Style a component using CSS Modules

In this section, you’ll create a list of people with names, avatars, and short Latin biographies. You’ll create a `<User />` component and style that component using a CSS module.

1. Create the file for the CSS at `src/pages/about-css-modules.module.css`.
2. Paste the following into the new file:

src/pages/about-css-modules.module.css

```css
Copysrc/pages/about-css-modules.module.css: copy code to clipboard
.user {
  display: flex;
  align-items: center;
  margin: 0 auto 12px auto;
}

.user:last-child {
  margin-bottom: 0;
}

.avatar {
  flex: 0 0 96px;
  width: 96px;
  height: 96px;
  margin: 0;
}

.description {
  flex: 1;
  margin-left: 18px;
  padding: 12px;
}

.username {
  margin: 0 0 12px 0;
  padding: 0;
}

.excerpt {
  margin: 0;
}
```

1. Import the new `src/pages/about-css-modules.module.css` file into the `about-css-modules.js` page you created earlier by editing the first few lines of the file like so:

src/pages/about-css-modules.js

```javascript
Copysrc/pages/about-css-modules.js: copy code to clipboard
import React from "react"
import styles from "./about-css-modules.module.css"
import Container from "../components/container"

console.log(styles)
```

The `console.log(styles)` code will log the resulting import so you can see the result of your processed `./about-css-modules.module.css` file. If you open the developer console (using e.g. Firefox or Chrome’s developer tools, often by the F12 key) in your browser, you’ll see:

[![Import result of CSS module in console](https://www.gatsbyjs.com/static/c1449b13fbeab2d990b6be27f26e364f/321ea/css-modules-console.png)](https://www.gatsbyjs.com/static/c1449b13fbeab2d990b6be27f26e364f/0e904/css-modules-console.png)

If you compare that to your CSS file, you’ll see that each class is now a key in the imported object pointing to a long string e.g. `avatar` points to `src-pages----about-css-modules-module---avatar---2lRF7`. These are the class names CSS Modules generates. They’re guaranteed to be unique across your site. And because you have to import them to use the classes, there’s never any question about where some CSS is being used.

1. Create a new `<User />` component inline in the `about-css-modules.js` page component. Modify `about-css-modules.js` so it looks like the following:

src/pages/about-css-modules.js

```jsx
Copysrc/pages/about-css-modules.js: copy code to clipboard
import React from "react"
import styles from "./about-css-modules.module.css"
import Container from "../components/container"

console.log(styles)

const User = props => (
  <div className={styles.user}>
    <img src={props.avatar} className={styles.avatar} alt="" />
    <div className={styles.description}>
      <h2 className={styles.username}>{props.username}</h2>
      <p className={styles.excerpt}>{props.excerpt}</p>
    </div>
  </div>
)

export default function About() {
  return (
    <Container>
      <h1>About CSS Modules</h1>
      <p>CSS Modules are cool</p>
      <User
        username="Jane Doe"
        avatar="https://s3.amazonaws.com/uifaces/faces/twitter/adellecharles/128.jpg"
        excerpt="I'm Jane Doe. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
      />
      <User
        username="Bob Smith"
        avatar="https://s3.amazonaws.com/uifaces/faces/twitter/vladarbatov/128.jpg"
        excerpt="I'm Bob Smith, a vertically aligned type of guy. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
      />
    </Container>
  )
}
```

> Tip: Generally, if you use a component in multiple places on a site, it should be in its own module file in the `components` directory. But, if it’s used only in one file, create it inline.

The finished page should now look like:

[![User list page with CSS modules](https://www.gatsbyjs.com/static/822dea21b09f9bc97e99eac926a778c7/321ea/css-modules-userlist.png)](https://www.gatsbyjs.com/static/822dea21b09f9bc97e99eac926a778c7/a4f81/css-modules-userlist.png)

### CSS-in-JS

CSS-in-JS is a component-oriented styling approach. Most generally, it is a pattern where [CSS is composed inline using JavaScript](https://reactjs.org/docs/faq-styling.html#what-is-css-in-js).

#### Using CSS-in-JS with Gatsby

There are many different CSS-in-JS libraries and many of them have Gatsby plugins already. We won’t cover an example of CSS-in-JS in this initial tutorial, but we encourage you to [explore](https://www.gatsbyjs.com/docs/styling/) what the ecosystem has to offer. There are mini-tutorials for two libraries, in particular, [Emotion](https://www.gatsbyjs.com/docs/how-to/styling/emotion/) and [Styled Components](https://www.gatsbyjs.com/docs/how-to/styling/styled-components/).

#### Suggested reading on CSS-in-JS

If you’re interested in further reading, check out [Christopher “vjeux” Chedeau’s 2014 presentation that sparked this movement](https://speakerdeck.com/vjeux/react-css-in-js) as well as [Mark Dalgleish’s more recent post “A Unified Styling Language”](https://medium.com/seek-blog/a-unified-styling-language-d0c208de2660).

### Other CSS options

Gatsby supports almost every possible styling option (if there isn’t a plugin yet for your favorite CSS option, [please contribute one!](https://www.gatsbyjs.com/contributing/how-to-contribute/))

- [Typography.js](https://www.gatsbyjs.com/packages/gatsby-plugin-typography/)
- [Sass](https://www.gatsbyjs.com/packages/gatsby-plugin-sass/)
- [JSS](https://www.gatsbyjs.com/packages/gatsby-plugin-jss/)
- [Stylus](https://www.gatsbyjs.com/packages/gatsby-plugin-stylus/)
- [PostCSS](https://www.gatsbyjs.com/packages/gatsby-plugin-postcss/)

and more!

## What’s coming next?

Now continue on to [part three of the tutorial](https://www.gatsbyjs.com/docs/tutorial/part-three/), where you’ll learn about Gatsby plugins and layout components.



# Creating Nested Layout Components

Welcome to part three!

## What’s in this tutorial?

In this part, you’ll learn about Gatsby plugins and creating “layout” components.

Gatsby plugins are JavaScript packages that help add functionality to a Gatsby site. Gatsby is designed to be extensible, which means plugins are able to extend and modify just about everything Gatsby does.

Layout components are for sections of your site that you want to share across multiple pages. For example, sites will commonly have a layout component with a shared header and footer. Other common things to add to layouts are a sidebar and/or navigation menu. On this page for example, the header at the top is part of gatsbyjs.com’s layout component.

Let’s dive into part three.

## Using plugins

You’re probably familiar with the idea of plugins. Many software systems support adding custom plugins to add new functionality or even modify the core workings of the software. Gatsby plugins work the same way.

Community members (like you!) can contribute plugins (small amounts of JavaScript code) that others can then use when building Gatsby sites.

> There are already hundreds of plugins! Explore the Gatsby [Plugin Library](https://www.gatsbyjs.com/plugins/).

Our goal with plugins is to make them straightforward to install and use. You will likely be using plugins in almost every Gatsby site you build. While working through the rest of the tutorial you’ll have many opportunities to practice installing and using plugins.

For an initial introduction to using plugins, we’ll install and implement the Gatsby plugin for Typography.js.

[Typography.js](https://kyleamathews.github.io/typography.js/) is a JavaScript library which generates global base styles for your site’s typography. The library has a [corresponding Gatsby plugin](https://www.gatsbyjs.com/packages/gatsby-plugin-typography/) to streamline using it in a Gatsby site.

### ✋ Create a new Gatsby site

As we mentioned in [part two](https://www.gatsbyjs.com/docs/tutorial/part-two/), at this point it’s probably a good idea to close the terminal window(s) and project files from previous parts of the tutorial, to keep things clean on your desktop. Then open a new terminal window and run the following commands to create a new Gatsby site in a directory called `tutorial-part-three` and then move to this new directory:

```shell

gatsby new tutorial-part-three https://github.com/gatsbyjs/gatsby-starter-hello-world
cd tutorial-part-three
```

### ✋ Install and configure `gatsby-plugin-typography`

There are two main steps to using a plugin: Installing and configuring.

1. Install the `gatsby-plugin-typography` npm package.

```shell

npm install gatsby-plugin-typography react-typography typography typography-theme-fairy-gates
```

> Note: Typography.js requires a few additional packages, so those are included in the instructions. Additional requirements like this will be listed in the “install” instructions of each plugin.

1. Edit the file `gatsby-config.js` at the root of your project to the following:

gatsby-config.js

```javascript
Copygatsby-config.js: copy code to clipboard
module.exports = {
  plugins: [
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
}
```

The `gatsby-config.js` is another special file that Gatsby will automatically recognize. This is where you add plugins and other site configuration.

> Check out the [doc on gatsby-config.js](https://www.gatsbyjs.com/docs/reference/config-files/gatsby-config/) to read more, if you wish.

1. Typography.js needs a configuration file. Create a new directory called `utils` in the `src` directory. Then add a new file called `typography.js` to `utils` and copy the following into the file:

src/utils/typography.js

```javascript
Copysrc/utils/typography.js: copy code to clipboard
import Typography from "typography"
import fairyGateTheme from "typography-theme-fairy-gates"

const typography = new Typography(fairyGateTheme)

export const { scale, rhythm, options } = typography
export default typography
```

1. Start the development server.

```shell

gatsby develop
```

Once you load the site, if you inspect the generated HTML using the Chrome developer tools, you’ll see that the typography plugin added a `<style>` element to the `<head>` element with its generated CSS:

[![Developer tool panel showing `typography.js` CSS styles](https://www.gatsbyjs.com/static/2c34a22832b1dd0828ac87fde925622a/321ea/typography-styles.png)](https://www.gatsbyjs.com/static/2c34a22832b1dd0828ac87fde925622a/04784/typography-styles.png)

### ✋ Make some content and style changes

Copy the following into your `src/pages/index.js` so you can see the effect of the CSS generated by Typography.js better.

src/pages/index.js

```jsx
Copysrc/pages/index.js: copy code to clipboard
import React from "react"

export default function Home() {
  return (
    <div>
      <h1>Hi! I'm building a fake Gatsby site as part of a tutorial!</h1>
      <p>
        What do I like to do? Lots of course but definitely enjoy building
        websites.
      </p>
    </div>
  )
}
```

Your site should now look like this:

[![Screenshot of site with no layout styling](https://www.gatsbyjs.com/static/95ba417a726c828267d5ca0f02cf0bb5/321ea/no-layout.png)](https://www.gatsbyjs.com/static/95ba417a726c828267d5ca0f02cf0bb5/ca3c3/no-layout.png)

Let’s make a quick improvement. Many sites have a single column of text centered in the middle of the page. To create this, add the following styles to the `<div>` in `src/pages/index.js`.

src/pages/index.js

```jsx
Copysrc/pages/index.js: copy code to clipboard
import React from "react"

export default function Home() {
  return (
    <div style={{ margin: `3rem auto`, maxWidth: 600 }}>
      <h1>Hi! I'm building a fake Gatsby site as part of a tutorial!</h1>
      <p>
        What do I like to do? Lots of course but definitely enjoy building
        websites.
      </p>
    </div>
  )
}
```

[![Screenshot of a Gatsby page with a centered column of text](https://www.gatsbyjs.com/static/a82222caf76c514d5ee974e197730fb1/321ea/with-layout2.png)](https://www.gatsbyjs.com/static/a82222caf76c514d5ee974e197730fb1/ca3c3/with-layout2.png)

Sweet. You’ve installed and configured your very first Gatsby plugin!

## Creating layout components

Now let’s move on to learning about layout components. To get ready for this part, add a couple new pages to your project: an about page and a contact page.

src/pages/about.js

```jsx
Copysrc/pages/about.js: copy code to clipboard
import React from "react"

export default function About() {
  return (
    <div>
      <h1>About me</h1>
      <p>
        I’m good enough, I’m smart enough, and gosh darn it, people like me!
      </p>
    </div>
  )
}
```

src/pages/contact.js

```jsx
Copysrc/pages/contact.js: copy code to clipboard
import React from "react"

export default function Contact() {
  return (
    <div>
      <h1>I'd love to talk! Email me at the address below</h1>
      <p>
        <a href="mailto:me@example.com">me@example.com</a>
      </p>
    </div>
  )
}
```

Let’s see what the new about page looks like:

[![About page with uncentered text](https://www.gatsbyjs.com/static/3f584fa0620c329508c29d35ccde9c30/321ea/about-uncentered.png)](https://www.gatsbyjs.com/static/3f584fa0620c329508c29d35ccde9c30/c4451/about-uncentered.png)

Hmm. It would be nice if the content of the two new pages were centered like the index page. And it would be nice to have some sort of global navigation so it’s easy for visitors to find and visit each of the sub-pages.

You’ll tackle these changes by creating your first layout component.

### ✋ Create your first layout component

1. Create a new directory at `src/components`.
2. Create a very basic layout component at `src/components/layout.js`:

src/components/layout.js

```jsx
Copysrc/components/layout.js: copy code to clipboard
import React from "react"

export default function Layout({ children }) {
  return (
    <div style={{ margin: `3rem auto`, maxWidth: 650, padding: `0 1rem` }}>
      {children}
    </div>
  )
}
```

1. Import this new layout component into your `src/pages/index.js` page component:

src/pages/index.js

```jsx
Copysrc/pages/index.js: copy code to clipboard
import React from "react"
import Layout from "../components/layout"

export default function Home() {
  return (
    <Layout>
      <h1>Hi! I'm building a fake Gatsby site as part of a tutorial!</h1>
      <p>
        What do I like to do? Lots of course but definitely enjoy building
        websites.
      </p>
    </Layout>
  );
}
```

[![Screenshot of a Gatsby page with a centered column of text](https://www.gatsbyjs.com/static/a82222caf76c514d5ee974e197730fb1/321ea/with-layout2.png)](https://www.gatsbyjs.com/static/a82222caf76c514d5ee974e197730fb1/ca3c3/with-layout2.png)

Sweet, the layout is working! The content of your index page is still centered.

But try navigating to `/about/`, or `/contact/`. The content on those pages still won’t be centered.

1. Import the layout component in `about.js` and `contact.js` (as you did for `index.js` in the previous step).

The content of all three of your pages is centered thanks to this single shared layout component!

### ✋ Add a site title

1. Add the following line to your new layout component:

src/components/layout.js

```jsx
Copysrc/components/layout.js: copy code to clipboard
import React from "react"

export default function Layout({ children }) {
  return (
    <div style={{ margin: `3rem auto`, maxWidth: 650, padding: `0 1rem` }}>
      <h3>MySweetSite</h3>
      {children}
    </div>
  )
}
```

If you go to any of your three pages, you’ll see the same title added, e.g. the `/about/` page:

[![Formatted page showing site title](https://www.gatsbyjs.com/static/edb105d20e6a8980efbf5313715dfb57/321ea/with-title.png)](https://www.gatsbyjs.com/static/edb105d20e6a8980efbf5313715dfb57/ca3c3/with-title.png)

### ✋ Add navigation links between pages

1. Copy the following into your layout component file:

src/components/layout.js

```jsx
Copysrc/components/layout.js: copy code to clipboard
import React from "react"
import { Link } from "gatsby"
const ListLink = props => (
  <li style={{ display: `inline-block`, marginRight: `1rem` }}>
    <Link to={props.to}>{props.children}</Link>
  </li>
)

export default function Layout({ children }) {
  return (
    <div style={{ margin: `3rem auto`, maxWidth: 650, padding: `0 1rem` }}>
      <header style={{ marginBottom: `1.5rem` }}>
        <Link to="/" style={{ textShadow: `none`, backgroundImage: `none` }}>
          <h3 style={{ display: `inline` }}>MySweetSite</h3>
        </Link>
        <ul style={{ listStyle: `none`, float: `right` }}>
          <ListLink to="/">Home</ListLink>
          <ListLink to="/about/">About</ListLink>
          <ListLink to="/contact/">Contact</ListLink>
        </ul>
      </header>
      {children}
    </div>
  )
}
```

[![A Gatsby page showing navigation links](https://www.gatsbyjs.com/static/420c464b89f35cb6394f134026fe3bc1/321ea/with-navigation.png)](https://www.gatsbyjs.com/static/420c464b89f35cb6394f134026fe3bc1/ca3c3/with-navigation.png)

And there you have it! A three page site with basic global navigation.

*Challenge:* With your new “layout component” powers, try adding headers, footers, global navigation, sidebars, etc. to your Gatsby sites!

## What’s coming next?

Continue on to [part four of the tutorial](https://www.gatsbyjs.com/docs/tutorial/part-four/) where you’ll start learning about Gatsby’s data layer and programmatically creating pages!



# Data in Gatsby

Welcome to Part Four of the tutorial! Halfway through! Hope things are starting to feel pretty comfortable 😀

## Recap of the first half of the tutorial

So far, you’ve been learning how to use React.js—how powerful it is to be able to create your *own* components to act as custom building blocks for websites.

You’ve also explored styling components using CSS Modules.

## What’s in this tutorial?

In the next four parts of the tutorial (including this one), you’ll be diving into the Gatsby data layer, which is a powerful feature of Gatsby that lets you build sites from Markdown, WordPress, headless CMSs, and other data sources of all flavors.

**NOTE:** Gatsby’s data layer is powered by GraphQL. For an in-depth tutorial on GraphQL, we recommend [How to GraphQL](https://www.howtographql.com/).

## Data in Gatsby

A website has four parts: HTML, CSS, JS, and data. The first half of the tutorial focused on the first three. Now let’s learn how to use data in Gatsby sites.

**What is data?**

A very computer science-y answer would be: data is things like `"strings"`, integers (`42`), objects (`{ pizza: true }`), etc.

For the purpose of working in Gatsby, however, a more useful answer is “everything that lives outside a React component”.

So far, you’ve been writing text and adding images *directly* in components. Which is an *excellent* way to build many websites. But, often you want to store data *outside* components and then bring the data *into* the component as needed.

If you’re building a site with WordPress (so other contributors have a nice interface for adding & maintaining content) and Gatsby, the *data* for the site (pages and posts) are in WordPress and you *pull* that data, as needed, into your components.

Data can also live in file types like Markdown, CSV, etc. as well as databases and APIs of all sorts.

**Gatsby’s data layer lets you pull data from these (and any other source) directly into your components** — in the shape and form you want.

## Using Unstructured Data vs GraphQL

### Do I have to use GraphQL and source plugins to pull data into Gatsby sites?

Absolutely not! You can use the node `createPages` API to pull unstructured data into Gatsby pages directly, rather than through the GraphQL data layer. This is a great choice for small sites, while GraphQL and source plugins can help save time with more complex sites.

See the [Using Gatsby without GraphQL](https://www.gatsbyjs.com/docs/how-to/querying-data/using-gatsby-without-graphql/) guide to learn how to pull data into your Gatsby site using the node `createPages` API and to see an example site!

### When do I use unstructured data vs GraphQL?

If you’re building a small site, one efficient way to build it is to pull in unstructured data as outlined in this guide, using `createPages` API, and then if the site becomes more complex later on, you move on to building more complex sites, or you’d like to transform your data, follow these steps:

1. Check out the [Plugin Library](https://www.gatsbyjs.com/plugins/) to see if the source plugins and/or transformer plugins you’d like to use already exist
2. If they don’t exist, read the [Plugin Authoring](https://www.gatsbyjs.com/docs/creating-plugins/) guide and consider building your own!

### How Gatsby’s data layer uses GraphQL to pull data into components

There are many options for loading data into React components. One of the most popular and powerful of these is a technology called [GraphQL](https://graphql.org/).

GraphQL was invented at Facebook to help product engineers *pull* needed data into components.

GraphQL is a **q**uery **l**anguage (the *QL* part of its name). If you’re familiar with SQL, it works in a very similar way. Using a special syntax, you describe the data you want in your component and then that data is given to you.

Gatsby uses GraphQL to enable components to declare the data they need.

## Create a new example site

Create another new site for this part of the tutorial. You’re going to build a Markdown blog called “Pandas Eating Lots”. It’s dedicated to showing off the best pictures and videos of pandas eating lots of food. Along the way, you’ll be dipping your toes into GraphQL and Gatsby’s Markdown support.

Open a new terminal window and run the following commands to create a new Gatsby site in a directory called `tutorial-part-four`. Then navigate to the new directory:

```shell

gatsby new tutorial-part-four https://github.com/gatsbyjs/gatsby-starter-hello-world
cd tutorial-part-four
```

Then install some other needed dependencies at the root of the project. You’ll use the Typography theme “Kirkham”, and you’ll try out a CSS-in-JS library, [“Emotion”](https://emotion.sh/):

```shell

npm install gatsby-plugin-typography typography react-typography typography-theme-kirkham gatsby-plugin-emotion @emotion/react
```

Set up a site similar to what you ended with in [Part Three](https://www.gatsbyjs.com/docs/tutorial/part-three). This site will have a layout component and two page components:

src/components/layout.js

```jsx
Copysrc/components/layout.js: copy code to clipboard
import React from "react"
import { css } from "@emotion/react"
import { Link } from "gatsby"

import { rhythm } from "../utils/typography"

export default function Layout({ children }) {
  return (
    <div
      css={css`
        margin: 0 auto;
        max-width: 700px;
        padding: ${rhythm(2)};
        padding-top: ${rhythm(1.5)};
      `}
    >
      <Link to={`/`}>
        <h3
          css={css`
            margin-bottom: ${rhythm(2)};
            display: inline-block;
            font-style: normal;
          `}
        >
          Pandas Eating Lots
        </h3>
      </Link>
      <Link
        to={`/about/`}
        css={css`
          float: right;
        `}
      >
        About
      </Link>
      {children}
    </div>
  )
}
```

src/pages/index.js

```jsx
Copysrc/pages/index.js: copy code to clipboard
import React from "react"
import Layout from "../components/layout"

export default function Home() {
  return (
    <Layout>
      <h1>Amazing Pandas Eating Things</h1>
      <div>
        <img
          src="https://2.bp.blogspot.com/-BMP2l6Hwvp4/TiAxeGx4CTI/AAAAAAAAD_M/XlC_mY3SoEw/s1600/panda-group-eating-bamboo.jpg"
          alt="Group of pandas eating bamboo"
        />
      </div>
    </Layout>
  )
}
```

src/pages/about.js

```jsx
Copysrc/pages/about.js: copy code to clipboard
import React from "react"
import Layout from "../components/layout"

export default function About() {
  return (
    <Layout>
      <h1>About Pandas Eating Lots</h1>
      <p>
        We're the only site running on your computer dedicated to showing the
        best photos and videos of pandas eating lots of food.
      </p>
    </Layout>
  )
}
```

src/utils/typography.js

```javascript
Copysrc/utils/typography.js: copy code to clipboard
import Typography from "typography"
import kirkhamTheme from "typography-theme-kirkham"

const typography = new Typography(kirkhamTheme)

export default typography
export const rhythm = typography.rhythm
```

`gatsby-config.js` (must be in the root of your project, not under src)

gatsby-config.js

```javascript
Copygatsby-config.js: copy code to clipboard
module.exports = {
  plugins: [
    `gatsby-plugin-emotion`,
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
}
```

Add the above files and then run `gatsby develop`, per usual, and you should see the following:

[![start](https://www.gatsbyjs.com/static/9a136a7536d2f4b315d446f6a1a83725/321ea/start.png)](https://www.gatsbyjs.com/static/9a136a7536d2f4b315d446f6a1a83725/ca3c3/start.png)

You have another small site with a layout and two pages.

Now you can start querying 😋

## Your first GraphQL query

When building sites, you’ll probably want to reuse common bits of data — like the *site title* for example. Look at the `/about/` page. You’ll notice that you have the site title (`Pandas Eating Lots`) in both the layout component (the site header) as well as in the `<h1 />` of the `about.js` page (the page header).

But what if you want to change the site title in the future? You’d have to search for the title across all your components and edit each instance. This is both cumbersome and error-prone, especially for larger, more complex sites. Instead, you can store the title in one location and reference that location from other files; change the title in a single place, and Gatsby will *pull* your updated title into files that reference it.

The place for these common bits of data is the `siteMetadata` object in the `gatsby-config.js` file. Add your site title to the `gatsby-config.js` file:

gatsby-config.js

```javascript
Copygatsby-config.js: copy code to clipboard
module.exports = {
  siteMetadata: {
    title: `Title from siteMetadata`,
  },
  plugins: [
    `gatsby-plugin-emotion`,
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
}
```

Restart the development server.

### Use a page query

Now the site title is available to be queried; Add it to the `about.js` file using a [page query](https://www.gatsbyjs.com/docs/how-to/querying-data/page-query):

src/pages/about.js

```jsx
Copysrc/pages/about.js: copy code to clipboard
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"

export default function About({ data }) {
  return (
    <Layout>
      <h1>About {data.site.siteMetadata.title}</h1>
      <p>
        We're the only site running on your computer dedicated to showing the
        best photos and videos of pandas eating lots of food.
      </p>
    </Layout>
  )
}

export const query = graphql`
  query {
    site {
      siteMetadata {
        title
      }
    }
  }
`
```

It worked! 🎉

[![Page title pulling from siteMetadata](https://www.gatsbyjs.com/static/4df7cdfeb994c1a07b4557f0f6010d91/c5bb3/site-metadata-title.png)](https://www.gatsbyjs.com/static/4df7cdfeb994c1a07b4557f0f6010d91/c5bb3/site-metadata-title.png)

The basic GraphQL query that retrieves the `title` in your `about.js` changes above is:

src/pages/about.js

```graphql
Copysrc/pages/about.js: copy code to clipboard
{
  site {
    siteMetadata {
      title
    }
  }
}
```

> 💡 In [part five](https://www.gatsbyjs.com/docs/tutorial/part-five/#introducing-graphiql), you’ll meet a tool that lets us interactively explore the data available through GraphQL, and help formulate queries like the one above.

Page queries live outside of the component definition — by convention at the end of a page component file — and are only available on page components.

### Use a StaticQuery

[StaticQuery](https://www.gatsbyjs.com/docs/how-to/querying-data/static-query/) is a new API introduced in Gatsby v2 that allows non-page components (like your `layout.js` component), to retrieve data via GraphQL queries. Let’s use its newly introduced hook version — [`useStaticQuery`](https://www.gatsbyjs.com/docs/how-to/querying-data/use-static-query/).

Go ahead and make some changes to your `src/components/layout.js` file to use the `useStaticQuery` hook and a `{data.site.siteMetadata.title}` reference that uses this data. When you are done, your file will look like this:

src/components/layout.js

```jsx
Copysrc/components/layout.js: copy code to clipboard
import React from "react"
import { css } from "@emotion/react"
import { useStaticQuery, Link, graphql } from "gatsby"

import { rhythm } from "../utils/typography"
export default function Layout({ children }) {
  const data = useStaticQuery(
    graphql`
      query {
        site {
          siteMetadata {
            title
          }
        }
      }
    `
  )
  return (
    <div
      css={css`
        margin: 0 auto;
        max-width: 700px;
        padding: ${rhythm(2)};
        padding-top: ${rhythm(1.5)};
      `}
    >
      <Link to={`/`}>
        <h3
          css={css`
            margin-bottom: ${rhythm(2)};
            display: inline-block;
            font-style: normal;
          `}
        >
          {data.site.siteMetadata.title}
        </h3>
      </Link>
      <Link
        to={`/about/`}
        css={css`
          float: right;
        `}
      >
        About
      </Link>
      {children}
    </div>
  )
}
```

Another success! 🎉

[![Page title and layout title both pulling from siteMetadata](https://www.gatsbyjs.com/static/500fd2f12d69813d2bbe6d669eaf3ce8/8ce52/site-metadata-two-titles.png)](https://www.gatsbyjs.com/static/500fd2f12d69813d2bbe6d669eaf3ce8/8ce52/site-metadata-two-titles.png)

Why use two different queries here? These examples were quick introductions to the query types, how they are formatted, and where they can be used. For now, keep in mind that only pages can make page queries. Non-page components, such as Layout, can use StaticQuery. [Part 7](https://www.gatsbyjs.com/docs/tutorial/part-seven/) of the tutorial explains these in greater depth.

But let’s restore the real title.

One of the core principles of Gatsby is that *creators need an immediate connection to what they’re creating* ([hat tip to Bret Victor](http://blog.ezyang.com/2012/02/transcript-of-inventing-on-principle/)). In other words, when you make any change to code you should immediately see the effect of that change. You manipulate an input of Gatsby and you see the new output showing up on the screen.

So almost everywhere, changes you make will immediately take effect. Edit the `gatsby-config.js` file again, this time changing the `title` back to “Pandas Eating Lots”. The change should show up very quickly in your site pages.

[![Both titles say Pandas Eating Lots](https://www.gatsbyjs.com/static/550fbd5e51d2ec54cad87687acb76a06/c5bb3/pandas-eating-lots-titles.png)](https://www.gatsbyjs.com/static/550fbd5e51d2ec54cad87687acb76a06/c5bb3/pandas-eating-lots-titles.png)

## What’s coming next?

Next, you’ll be learning about how to pull data into your Gatsby site using GraphQL with source plugins in [part five](https://www.gatsbyjs.com/docs/tutorial/part-five/) of the tutorial.



# Source Plugins

> This tutorial is part of a series about Gatsby’s data layer. Make sure you’ve gone through [part 4](https://www.gatsbyjs.com/docs/tutorial/part-four/) before continuing here.

## What’s in this tutorial?

In this tutorial, you’ll be learning about how to pull data into your Gatsby site using GraphQL and source plugins. Before you learn about these plugins, however, you’ll want to know how to use something called GraphiQL, a tool that helps you structure your queries correctly.

## Introducing GraphiQL

GraphiQL is the GraphQL integrated development environment (IDE). It’s a powerful (and all-around awesome) tool you’ll use often while building Gatsby websites.

You can access it when your site’s development server is running—normally at `http://localhost:8000/___graphql`.

<video controls="" autoplay="" loop="" style="box-sizing: inherit; display: inline-block; width: 702px; margin-bottom: 1.5rem;"></video>

Poke around the built-in `Site` “type” and see what fields are available on it — including the `siteMetadata` object you queried earlier. Try opening GraphiQL and play with your data! Press Ctrl + Space (or use Shift + Space as an alternate keyboard shortcut) to bring up the autocomplete window and Ctrl + Enter to run the GraphQL query. You’ll be using GraphiQL a lot more through the remainder of the tutorial.

## Using the GraphiQL Explorer

The GraphiQL Explorer enables you to interactively construct full queries by clicking through available fields and inputs without the repetitive process of typing these queries out by hand.

<iframe class="egghead-video" width="600" height="337.5" src="https://egghead.io/lessons/gatsby-build-a-graphql-query-using-gatsby-s-graphiql-explorer/embed" title="Video: Build a GraphQL Query using Gatsby’s GraphiQL Explorer" allowfullscreen="" style="box-sizing: inherit; margin: 0px 0px 1.5rem; padding: 0px; border: none; max-width: 100%;"></iframe>

*Video hosted on [egghead.io](https://egghead.io/lessons/gatsby-build-a-graphql-query-using-gatsby-s-graphiql-explorer)*.

## Source plugins

Data in Gatsby sites can come from anywhere: APIs, databases, CMSs, local files, etc.

Source plugins fetch data from their source. E.g. the filesystem source plugin knows how to fetch data from the file system. The WordPress plugin knows how to fetch data from the WordPress API.

Add [`gatsby-source-filesystem`](https://www.gatsbyjs.com/packages/gatsby-source-filesystem/) and explore how it works.

First, install the plugin at the root of the project:

```shell

npm install gatsby-source-filesystem
```

Then add it to your `gatsby-config.js`:

gatsby-config.js

```javascript
Copygatsby-config.js: copy code to clipboard
module.exports = {
  siteMetadata: {
    title: `Pandas Eating Lots`,
  },
  plugins: [
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `src`,
        path: `${__dirname}/src/`,
      },
    },
    `gatsby-plugin-emotion`,
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
}
```

Save that and restart the gatsby development server. Then open up GraphiQL again.

In the explorer pane, you’ll see `allFile` and `file` available as selections:

[![The GraphiQL IDE showing the new dropdown options provided by the gatsby-source-filesystem plugin](https://www.gatsbyjs.com/static/88ec3efe94e380d32bc1a20cd82dd8bf/321ea/graphiql-filesystem.png)](https://www.gatsbyjs.com/static/88ec3efe94e380d32bc1a20cd82dd8bf/373fb/graphiql-filesystem.png)

Click the `allFile` dropdown. Position your cursor after `allFile` in the query area, and then type Ctrl + Enter. This will pre-fill a query for the `id` of each file. Press “Play” to run the query:

[![The GraphiQL IDE showing the results of a filesystem query](https://www.gatsbyjs.com/static/cf2ffc2f9d3aa512fb742efd377691da/321ea/filesystem-query.png)](https://www.gatsbyjs.com/static/cf2ffc2f9d3aa512fb742efd377691da/1d7f7/filesystem-query.png)

In the Explorer pane, the `id` field has automatically been selected. Make selections for more fields by checking the field’s corresponding checkbox. Press “Play” to run the query again, with the new fields:

[![The GraphiQL IDE showing the new fields in the Explorer column](https://www.gatsbyjs.com/static/d430ba8bcbc8eb92cd549b70f3798561/321ea/filesystem-explorer-options.png)](https://www.gatsbyjs.com/static/d430ba8bcbc8eb92cd549b70f3798561/10c1e/filesystem-explorer-options.png)

Alternatively, you can add fields by using the autocomplete shortcut (Ctrl + Space). This will show queryable fields on the `File` nodes.

[![The GraphiQL IDE showing the gatsby-source-filesystem plugin's new autocomplete options](https://www.gatsbyjs.com/static/b2b05958c518b34568861f40449228f4/321ea/filesystem-autocomplete.png)](https://www.gatsbyjs.com/static/b2b05958c518b34568861f40449228f4/8c48a/filesystem-autocomplete.png)

Try adding a number of fields to your query, press Ctrl + Enter each time to re-run the query. You’ll see the updated query results:

[![The GraphiQL IDE showing the results of the query](https://www.gatsbyjs.com/static/077caa982416bc5df87e31f21a1a3417/321ea/allfile-query.png)](https://www.gatsbyjs.com/static/077caa982416bc5df87e31f21a1a3417/eff3b/allfile-query.png)

The result is an array of `File` “nodes” (node is a fancy name for an object in a “graph”). Each `File` node object has the fields you queried for.

## Build a page with a GraphQL query

Building new pages with Gatsby often starts in GraphiQL. You first sketch out the data query by playing in GraphiQL then copy this to a React page component to start building the UI.

Let’s try this.

Create a new file at `src/pages/my-files.js` with the `allFile` GraphQL query you just created:

src/pages/my-files.js

```jsx
Copysrc/pages/my-files.js: copy code to clipboard
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"

export default function MyFiles({ data }) {
  console.log(data)
  return (
    <Layout>
      <div>Hello world</div>
    </Layout>
  )
}

export const query = graphql`
  query {
    allFile {
      edges {
        node {
          relativePath
          prettySize
          extension
          birthTime(fromNow: true)
        }
      }
    }
  }
`
```

The `console.log(data)` line is highlighted above. It’s often helpful when creating a new component to console out the data you’re getting from the GraphQL query so you can explore the data in your browser console while building the UI.

If you visit the new page at `/my-files/` and open up your browser console you will see something like:

[![Browser console showing the structure of the data object](https://www.gatsbyjs.com/static/3fd681a2f33d483a82d067b07704f7e5/321ea/data-in-console.png)](https://www.gatsbyjs.com/static/3fd681a2f33d483a82d067b07704f7e5/fbf08/data-in-console.png)

The shape of the data matches the shape of the GraphQL query.

Add some code to your component to print out the File data.

src/pages/my-files.js

```jsx
Copysrc/pages/my-files.js: copy code to clipboard
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"

export default function MyFiles({ data }) {
  console.log(data)
  return (
    <Layout>
      <div>
        <h1>My Site's Files</h1>
        <table>
          <thead>
            <tr>
              <th>relativePath</th>
              <th>prettySize</th>
              <th>extension</th>
              <th>birthTime</th>
            </tr>
          </thead>
          <tbody>
            {data.allFile.edges.map(({ node }, index) => (
              <tr key={index}>
                <td>{node.relativePath}</td>
                <td>{node.prettySize}</td>
                <td>{node.extension}</td>
                <td>{node.birthTime}</td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
    </Layout>
  )
}

export const query = graphql`
  query {
    allFile {
      edges {
        node {
          relativePath
          prettySize
          extension
          birthTime(fromNow: true)
        }
      }
    }
  }
`
```

And now visit `http://localhost:8000/my-files`… 😲

[![A browser window showing a list of the files in the site](https://www.gatsbyjs.com/static/d5507ac06a742b5fe3a91a40f9c3148a/321ea/my-files-page.png)](https://www.gatsbyjs.com/static/d5507ac06a742b5fe3a91a40f9c3148a/1ffbd/my-files-page.png)

## What’s coming next?

Now you’ve learned how source plugins bring data *into* Gatsby’s data system. In the next tutorial, you’ll learn how transformer plugins *transform* the raw content brought by source plugins. The combination of source plugins and transformer plugins can handle all data sourcing and data transformation you might need when building a Gatsby site. Learn about transformer plugins in [part six of the tutorial](https://www.gatsbyjs.com/docs/tutorial/part-six/).



# Transformer plugins

> This tutorial is part of a series about Gatsby’s data layer. Make sure you’ve gone through [part 4](https://www.gatsbyjs.com/docs/tutorial/part-four/) and [part 5](https://www.gatsbyjs.com/docs/tutorial/part-five/) before continuing here.

## What’s in this tutorial?

The previous tutorial showed how source plugins bring data *into* Gatsby’s data system. In this tutorial, you’ll learn how transformer plugins *transform* the raw content brought by source plugins. The combination of source plugins and transformer plugins can handle all data sourcing and data transformation you might need when building a Gatsby site.

## Transformer plugins

Often, the format of the data you get from source plugins isn’t what you want to use to build your website. The filesystem source plugin lets you query data *about* files but what if you want to query data *inside* files?

To make this possible, Gatsby supports transformer plugins which take raw content from source plugins and *transform* it into something more usable.

For example, markdown files. Markdown is nice to write in but when you build a page with it, you need the markdown to be HTML.

Add a markdown file to your site at `src/pages/sweet-pandas-eating-sweets.md` (This will become your first markdown blog post) and learn how to *transform* it to HTML using transformer plugins and GraphQL.

src/pages/sweet-pandas-eating-sweets.md

```markdown
Copysrc/pages/sweet-pandas-eating-sweets.md: copy code to clipboard
---
title: "Sweet Pandas Eating Sweets"
date: "2017-08-10"
---

Pandas are really sweet.

Here's a video of a panda eating sweets.

<iframe width="560" height="315" src="https://www.youtube.com/embed/4n0xNbfJLR8" frameborder="0" allowfullscreen></iframe>
```

Once you save the file, look at `/my-files/` again—the new markdown file is in the table. This is a very powerful feature of Gatsby. Like the earlier `siteMetadata` example, source plugins can live-reload data. `gatsby-source-filesystem` is always scanning for new files to be added and when they are, re-runs your queries.

Add a transformer plugin that can transform markdown files:

```shell

npm install gatsby-transformer-remark
```

Then add it to the `gatsby-config.js` like normal:

gatsby-config.js

```javascript
Copygatsby-config.js: copy code to clipboard
module.exports = {
  siteMetadata: {
    title: `Pandas Eating Lots`,
  },
  plugins: [
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `src`,
        path: `${__dirname}/src/`,
      },
    },
    `gatsby-transformer-remark`,
    `gatsby-plugin-emotion`,
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
}
```

Restart the development server then refresh (or open again) GraphiQL and look at the autocomplete:

[![GraphiQL screenshot showing new `gatsby-transformer-remark` autocomplete options](https://www.gatsbyjs.com/static/646695e05a4aafdf903b727c8013f6b7/321ea/markdown-autocomplete.png)](https://www.gatsbyjs.com/static/646695e05a4aafdf903b727c8013f6b7/7bf07/markdown-autocomplete.png)

Select `allMarkdownRemark` again and run it as you did for `allFile`. You’ll see there the markdown file you recently added. Explore the fields that are available on the `MarkdownRemark` node.

[![GraphiQL screenshot showing the result of a query](https://www.gatsbyjs.com/static/26081bb3e08de00f1d878b807b552daf/321ea/markdown-query.png)](https://www.gatsbyjs.com/static/26081bb3e08de00f1d878b807b552daf/ca3c3/markdown-query.png)

Ok! Hopefully, some basics are starting to fall into place. Source plugins bring data *into* Gatsby’s data system and *transformer* plugins transform raw content brought by source plugins. This pattern can handle all data sourcing and data transformation you might need when building a Gatsby site.

## Create a list of your site’s markdown files in `src/pages/index.js`

Now you’ll have to create a list of your markdown files on the front page. Like many blogs, you want to end up with a list of links on the front page pointing to each blog post. With GraphQL you can *query* for the current list of markdown blog posts so you won’t need to maintain the list manually.

Like with the `src/pages/my-files.js` page, replace `src/pages/index.js` with the following to add a GraphQL query with some initial HTML and styling.

src/pages/index.js

```jsx
Copysrc/pages/index.js: copy code to clipboard
import React from "react"
import { graphql } from "gatsby"
import { css } from "@emotion/react"
import { rhythm } from "../utils/typography"
import Layout from "../components/layout"

export default function Home({ data }) {
  console.log(data)
  return (
    <Layout>
      <div>
        <h1
          css={css`
            display: inline-block;
            border-bottom: 1px solid;
          `}
        >
          Amazing Pandas Eating Things
        </h1>
        <h4>{data.allMarkdownRemark.totalCount} Posts</h4>
        {data.allMarkdownRemark.edges.map(({ node }) => (
          <div key={node.id}>
            <h3
              css={css`
                margin-bottom: ${rhythm(1 / 4)};
              `}
            >
              {node.frontmatter.title}{" "}
              <span
                css={css`
                  color: #bbb;
                `}
              >
                — {node.frontmatter.date}
              </span>
            </h3>
            <p>{node.excerpt}</p>
          </div>
        ))}
      </div>
    </Layout>
  )
}

export const query = graphql`
  query {
    allMarkdownRemark {
      totalCount
      edges {
        node {
          id
          frontmatter {
            title
            date(formatString: "DD MMMM, YYYY")
          }
          excerpt
        }
      }
    }
  }
`
```

Now the frontpage should look like:

[![Screenshot of the frontpage](https://www.gatsbyjs.com/static/c12c3c281af8226af74349e0f316b797/321ea/frontpage.png)](https://www.gatsbyjs.com/static/c12c3c281af8226af74349e0f316b797/ca3c3/frontpage.png)

But your one blog post looks a bit lonely. So let’s add another one at `src/pages/pandas-and-bananas.md`

src/pages/pandas-and-bananas.md

```markdown
Copysrc/pages/pandas-and-bananas.md: copy code to clipboard
---
title: "Pandas and Bananas"
date: "2017-08-21"
---

Do Pandas eat bananas? Check out this short video that shows that yes! pandas do seem to really enjoy bananas!

<iframe width="560" height="315" src="https://www.youtube.com/embed/4SZl1r2O_bY" frameborder="0" allowfullscreen></iframe>
```

[![Frontpage showing two posts](https://www.gatsbyjs.com/static/d7b4537b69b87253593231268802baaa/321ea/two-posts.png)](https://www.gatsbyjs.com/static/d7b4537b69b87253593231268802baaa/ca3c3/two-posts.png)

Which looks great! Except… the order of the posts is wrong.

But this is easy to fix. When querying a connection of some type, you can pass a variety of arguments to the GraphQL query. You can `sort` and `filter` nodes, set how many nodes to `skip`, and choose the `limit` of how many nodes to retrieve. With this powerful set of operators, you can select any data you want—in the format you need.

In your index page’s GraphQL query, change `allMarkdownRemark` to `allMarkdownRemark(sort: { fields: [frontmatter___date], order: DESC })`. *Note: There are 3 underscores between `frontmatter` and `date`.* Save this and the sort order should be fixed.

Try opening GraphiQL and playing with different sort options. You can sort the `allFile` connection along with other connections.

For more documentation on our query operators, explore our [GraphQL reference guide.](https://www.gatsbyjs.com/docs/graphql-reference/)

## Challenge

Try creating a new page containing a blog post and see what happens to the list of blog posts on the homepage!

## What’s coming next?

This is great! You’ve just created a nice index page where you’re querying your markdown files and producing a list of blog post titles and excerpts. But you don’t want to just see excerpts, you want actual pages for your markdown files.

You could continue to create pages by placing React components in `src/pages`. However, you’ll next learn how to *programmatically* create pages from *data*. Gatsby is *not* limited to making pages from files like many static site generators. Gatsby lets you use GraphQL to query your *data* and *map* the query results to *pages*—all at build time. This is a really powerful idea. You’ll be exploring its implications and ways to use it in the next tutorial, where you’ll learn how to [programmatically create pages from data](https://www.gatsbyjs.com/docs/tutorial/part-seven/).



# Programmatically create pages from data

> This tutorial is part of a series about Gatsby’s data layer. Make sure you’ve gone through [part 4](https://www.gatsbyjs.com/docs/tutorial/part-four/), [part 5](https://www.gatsbyjs.com/docs/tutorial/part-five/), and [part 6](https://www.gatsbyjs.com/docs/tutorial/part-six/) before continuing here.

## What’s in this tutorial?

In the previous tutorial, you created a nice index page that queries markdown files and produces a list of blog post titles and excerpts. But you don’t want to just see excerpts, you want actual pages for your markdown files.

You could continue to create pages by placing React components in `src/pages`. However, you’ll now learn how to *programmatically* create pages from *data*. Gatsby is *not* limited to making pages from files like many static site generators. Gatsby lets you use GraphQL to query your *data* and *map* the query results to *pages*—all at build time. This is a really powerful idea. You’ll be exploring its implications and ways to use it for the remainder of this part of the tutorial.

Let’s get started.

## Creating slugs for pages

A ‘slug’ is the unique identifying part of a web address, such as the `/docs/tutorial/part-seven` part of the page `https://www.gatsbyjs.com/docs/tutorial/part-seven/`.

It is also referred to as the ‘path’ but this tutorial will use the term ‘slug’ for consistency.

Creating new pages has two steps:

1. Generate the “path” or “slug” for the page.
2. Create the page.

***Note**: Often data sources will directly provide a slug or pathname for content — when working with one of those systems (e.g. a CMS), you don’t need to create the slugs yourself as you do with markdown files.*

To create your markdown pages, you’ll learn to use two Gatsby APIs: [`onCreateNode`](https://www.gatsbyjs.com/docs/reference/config-files/gatsby-node/#onCreateNode) and [`createPages`](https://www.gatsbyjs.com/docs/reference/config-files/gatsby-node/#createPages). These are two workhorse APIs you’ll see used in many sites and plugins.

We do our best to make Gatsby APIs simple to implement. To implement an API, you export a function with the name of the API from `gatsby-node.js`.

So, here’s where you’ll do that. In the root of your site, create a file named `gatsby-node.js`. Then add the following.

gatsby-node.js

```javascript
Copygatsby-node.js: copy code to clipboard
exports.onCreateNode = ({ node }) => {
  console.log(`Node created of type "${node.internal.type}"`)
}
```

This `onCreateNode` function will be called by Gatsby whenever a new node is created (or updated).

Stop and restart the development server. As you do, you’ll see quite a few newly created nodes get logged to the terminal console.

In the next section, you will use this API to add slugs for your Markdown pages to `MarkdownRemark` nodes.

Change your function so it now only logs `MarkdownRemark` nodes.

gatsby-node.js

```javascript
Copygatsby-node.js: copy code to clipboard
exports.onCreateNode = ({ node }) => {
  if (node.internal.type === `MarkdownRemark`) {
    console.log(node.internal.type)
  }
}
```

You want to use each markdown file name to create the page slug. So `pandas-and-bananas.md` will become `/pandas-and-bananas/`. But how do you get the file name from the `MarkdownRemark` node? To get it, you need to *traverse* the “node graph” to its *parent* `File` node, as `File` nodes contain data you need about files on disk. To do that, you’ll use the [`getNode()`](https://www.gatsbyjs.com/docs/reference/config-files/node-api-helpers/#getNode) helper. Add it to `onCreateNode`’s function parameters, and call it to get the file node:

gatsby-node.js

```javascript
Copygatsby-node.js: copy code to clipboard
exports.onCreateNode = ({ node, getNode }) => {
  if (node.internal.type === `MarkdownRemark`) {
    const fileNode = getNode(node.parent)
    console.log(`\n`, fileNode.relativePath)
  }
}
```

After restarting your development server, you should see the relative paths for your two markdown files print to the terminal screen.

[![markdown-relative-path](https://www.gatsbyjs.com/static/01e3ab44062c37f7f8c749101e8b8915/4971b/markdown-relative-path.png)](https://www.gatsbyjs.com/static/01e3ab44062c37f7f8c749101e8b8915/4971b/markdown-relative-path.png)

Now you’ll have to create slugs. As the logic for creating slugs from file names can get tricky, the `gatsby-source-filesystem` plugin ships with a function for creating slugs. Let’s use that.

gatsby-node.js

```javascript
Copygatsby-node.js: copy code to clipboard
const { createFilePath } = require(`gatsby-source-filesystem`)

exports.onCreateNode = ({ node, getNode }) => {
  if (node.internal.type === `MarkdownRemark`) {
    console.log(createFilePath({ node, getNode, basePath: `pages` }))
  }
}
```

The function handles finding the parent `File` node along with creating the slug. Run the development server again and you should see logged to the terminal two slugs, one for each markdown file.

Now you can add your new slugs directly onto the `MarkdownRemark` nodes. This is powerful, as any data you add to nodes is available to query later with GraphQL. So, it’ll be easy to get the slug when it comes time to create the pages.

To do so, you’ll use a function passed to your API implementation called [`createNodeField`](https://www.gatsbyjs.com/docs/reference/config-files/actions/#createNodeField). This function allows you to create additional fields on nodes created by other plugins. Only the original creator of a node can directly modify the node—all other plugins (including your `gatsby-node.js`) must use this function to create additional fields.

gatsby-node.js

```javascript
Copygatsby-node.js: copy code to clipboard
const { createFilePath } = require(`gatsby-source-filesystem`)
exports.onCreateNode = ({ node, getNode, actions }) => {
  const { createNodeField } = actions
  if (node.internal.type === `MarkdownRemark`) {
    const slug = createFilePath({ node, getNode, basePath: `pages` })
    createNodeField({
      node,
      name: `slug`,
      value: slug,
    })
  }
}
```

Restart the development server and open or refresh GraphiQL. Then run this GraphQL query to see your new slugs.

```graphql

{
  allMarkdownRemark {
    edges {
      node {
        fields {
          slug
        }
      }
    }
  }
}
```

Now that the slugs are created, you can create the pages.

## Creating pages

In the same `gatsby-node.js` file, add the following.

gatsby-node.js

```javascript
Copygatsby-node.js: copy code to clipboard
const { createFilePath } = require(`gatsby-source-filesystem`)

exports.onCreateNode = ({ node, getNode, actions }) => {
  const { createNodeField } = actions
  if (node.internal.type === `MarkdownRemark`) {
    const slug = createFilePath({ node, getNode, basePath: `pages` })
    createNodeField({
      node,
      name: `slug`,
      value: slug,
    })
  }
}

exports.createPages = async ({ graphql, actions }) => {
  // **Note:** The graphql function call returns a Promise
  // see: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise for more info
  const result = await graphql(`
    query {
      allMarkdownRemark {
        edges {
          node {
            fields {
              slug
            }
          }
        }
      }
    }
  `)
  console.log(JSON.stringify(result, null, 4))
}
```

You’ve added an implementation of the [`createPages`](https://www.gatsbyjs.com/docs/reference/config-files/gatsby-node/#createPages) API which Gatsby calls so plugins can add pages.

As mentioned in the intro to this part of the tutorial, the steps to programmatically creating pages are:

1. Query data with GraphQL
2. Map the query results to pages

The above code is the first step for creating pages from your markdown as you’re using the supplied `graphql` function to query the markdown slugs you created. Then you’re logging out the result of the query which should look like:

[![query-markdown-slugs](https://www.gatsbyjs.com/static/5193a6c95058806213c59a7bcf73d526/321ea/query-markdown-slugs.png)](https://www.gatsbyjs.com/static/5193a6c95058806213c59a7bcf73d526/84bf8/query-markdown-slugs.png)

You need one additional thing beyond a slug to create pages: a page template component. Like everything in Gatsby, programmatic pages are powered by React components. When creating a page, you need to specify which component to use.

Create a directory at `src/templates`, and then add the following in a file named `src/templates/blog-post.js`.

src/templates/blog-post.js

```jsx
Copysrc/templates/blog-post.js: copy code to clipboard
import React from "react"
import Layout from "../components/layout"

export default function BlogPost() {
  return (
    <Layout>
      <div>Hello blog post</div>
    </Layout>
  )
}
```

Then update `gatsby-node.js`

gatsby-node.js

```javascript
Copygatsby-node.js: copy code to clipboard
const path = require(`path`)
const { createFilePath } = require(`gatsby-source-filesystem`)

exports.onCreateNode = ({ node, getNode, actions }) => {
  const { createNodeField } = actions
  if (node.internal.type === `MarkdownRemark`) {
    const slug = createFilePath({ node, getNode, basePath: `pages` })
    createNodeField({
      node,
      name: `slug`,
      value: slug,
    })
  }
}

exports.createPages = async ({ graphql, actions }) => {
  const { createPage } = actions
  const result = await graphql(`
    query {
      allMarkdownRemark {
        edges {
          node {
            fields {
              slug
            }
          }
        }
      }
    }
  `)

  result.data.allMarkdownRemark.edges.forEach(({ node }) => {
    createPage({
      path: node.fields.slug,
      component: path.resolve(`./src/templates/blog-post.js`),
      context: {
        // Data passed to context is available
        // in page queries as GraphQL variables.
        slug: node.fields.slug,
      },
    })
  })
}
```

Restart the development server and your pages will be created! An easy way to find new pages you create while developing is to go to a random path where Gatsby will helpfully show you a list of pages on the site. If you go to `http://localhost:8000/sdf`, you’ll see the new pages you created.

[![new-pages](https://www.gatsbyjs.com/static/b1a3666651a4de0eaf754938d4c9e4fb/321ea/new-pages.png)](https://www.gatsbyjs.com/static/b1a3666651a4de0eaf754938d4c9e4fb/ca3c3/new-pages.png)

Visit one of them and you see:

[![hello-world-blog-post](https://www.gatsbyjs.com/static/3467d825ce4845fabbec061e8130e0a8/321ea/hello-world-blog-post.png)](https://www.gatsbyjs.com/static/3467d825ce4845fabbec061e8130e0a8/ca3c3/hello-world-blog-post.png)

Which is a bit boring and not what you want. Now you can pull in data from your markdown post. Change `src/templates/blog-post.js` to:

src/templates/blog-post.js

```jsx
Copysrc/templates/blog-post.js: copy code to clipboard
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"

export default function BlogPost({ data }) {
  const post = data.markdownRemark
  return (
    <Layout>
      <div>
        <h1>{post.frontmatter.title}</h1>
        <div dangerouslySetInnerHTML={{ __html: post.html }} />
      </div>
    </Layout>
  )
}

export const query = graphql`
  query($slug: String!) {
    markdownRemark(fields: { slug: { eq: $slug } }) {
      html
      frontmatter {
        title
      }
    }
  }
`
```

And…

[![blog-post](https://www.gatsbyjs.com/static/d91348f58c91ccc92588a68be507b324/321ea/blog-post.png)](https://www.gatsbyjs.com/static/d91348f58c91ccc92588a68be507b324/ca3c3/blog-post.png)

Sweet!

The last step is to link to your new pages from the index page.

Return to `src/pages/index.js`, query for your markdown slugs, and create links.

src/pages/index.js

```jsx
Copysrc/pages/index.js: copy code to clipboard
import React from "react"
import { css } from "@emotion/react"
import { Link, graphql } from "gatsby"
import { rhythm } from "../utils/typography"
import Layout from "../components/layout"

export default function Home({ data }) {
  return (
    <Layout>
      <div>
        <h1
          css={css`
            display: inline-block;
            border-bottom: 1px solid;
          `}
        >
          Amazing Pandas Eating Things
        </h1>
        <h4>{data.allMarkdownRemark.totalCount} Posts</h4>
        {data.allMarkdownRemark.edges.map(({ node }) => (
          <div key={node.id}>
            <Link
              to={node.fields.slug}
              css={css`
                text-decoration: none;
                color: inherit;
              `}
            >
              <h3
                css={css`
                  margin-bottom: ${rhythm(1 / 4)};
                `}
              >
                {node.frontmatter.title}{" "}
                <span
                  css={css`
                    color: #555;
                  `}
                >
                  — {node.frontmatter.date}
                </span>
              </h3>
              <p>{node.excerpt}</p>
            </Link>
          </div>
        ))}
      </div>
    </Layout>
  )
}

export const query = graphql`
  query {
    allMarkdownRemark(sort: { fields: [frontmatter___date], order: DESC }) {
      totalCount
      edges {
        node {
          id
          frontmatter {
            title
            date(formatString: "DD MMMM, YYYY")
          }
          fields {
            slug
          }
          excerpt
        }
      }
    }
  }
`
```

And there you go! A working, albeit small, blog!

## Challenge

Try playing more with the site. Try adding some more markdown files. Explore querying other data from the `MarkdownRemark` nodes and adding them to the front page or blog posts pages.

In this part of the tutorial, you’ve learned the foundations of building with Gatsby’s data layer. You’ve learned how to *source* and *transform* data using plugins, how to use GraphQL to *map* data to pages, and then how to build *page template components* where you query for data for each page.

## What’s coming next?

Now that you’ve built a Gatsby site, where do you go next?

- Share your Gatsby site on Twitter and see what other people have created by searching for #gatsbytutorial! Make sure to mention @gatsbyjs in your Tweet and include the hashtag #gatsbytutorial :)
- You could take a look at some [example sites](https://github.com/gatsbyjs/gatsby/tree/master/examples#gatsby-example-websites)
- Explore more [plugins](https://www.gatsbyjs.com/docs/plugins/)
- See what [other people are building with Gatsby](https://www.gatsbyjs.com/showcase/)
- Check out the documentation on [Gatsby’s APIs](https://www.gatsbyjs.com/docs/api-specification/), [nodes](https://www.gatsbyjs.com/docs/reference/graphql-data-layer/node-interface/), or [GraphQL](https://www.gatsbyjs.com/docs/graphql-reference/)



# Preparing a Site to Go Live

Wow! You’ve come a long way! You’ve learned how to:

- create new Gatsby sites
- create pages and components
- style components
- add plugins to a site
- source & transform data
- use GraphQL to query data for pages
- programmatically create pages from your data

In this final section, you’re going to walk through some common steps for preparing a site to go live by introducing a powerful site diagnostic tool called [Lighthouse](https://developers.google.com/web/tools/lighthouse/). Along the way, we’ll introduce a few more plugins you’ll often want to use in your Gatsby sites.

## Audit with Lighthouse

Quoting from the [Lighthouse website](https://developers.google.com/web/tools/lighthouse/):

> Lighthouse is an open-source, automated tool for improving the quality of web pages. You can run it against any web page, public or requiring authentication. It has audits for performance, accessibility, progressive web apps (PWAs), and more.

Lighthouse is included in Chrome DevTools. Running its audit — and then addressing the errors it finds and implementing the improvements it suggests — is a great way to prepare your site to go live. It helps give you confidence that your site is as fast and accessible as possible.

Try it out!

First, you need to create a production build of your Gatsby site. The Gatsby development server is optimized for making development fast; But the site that it generates, while closely resembling a production version of the site, isn’t as optimized.

### ✋ Create a production build

1. Stop the development server (if it’s still running) and run the following command:

```shell

gatsby build
```

> 💡 As you learned in [part 1](https://www.gatsbyjs.com/docs/tutorial/part-one/), this does a production build of your site and outputs the built static files into the `public` directory.

1. View the production site locally. Run:

```shell

gatsby serve
```

Once this starts, you can view your site at `http://localhost:9000`.

### Run a Lighthouse audit

Now you’re going to run your first Lighthouse test.

1. If you haven’t already done so, open the site in Chrome Incognito Mode so no extensions interfere with the test. Then, open up the Chrome DevTools.
2. Click on the “Audits” tab where you’ll see a screen that looks like:

[![Lighthouse audit start](https://www.gatsbyjs.com/static/cdc985b7497f4a6b99b6bbd19f9168fa/321ea/lighthouse-audit.png)](https://www.gatsbyjs.com/static/cdc985b7497f4a6b99b6bbd19f9168fa/df56e/lighthouse-audit.png)

1. Click “Perform an audit…” (All available audit types should be selected by default). Then click “Run audit”. (It’ll then take a minute or so to run the audit). Once the audit is complete, you should see results that look like this:

[![Lighthouse audit results](https://www.gatsbyjs.com/static/46b36f48f05e2a3ce358991fe95c5446/321ea/lighthouse-audit-results.png)](https://www.gatsbyjs.com/static/46b36f48f05e2a3ce358991fe95c5446/d7ceb/lighthouse-audit-results.png)

As you can see, Gatsby’s performance is excellent out of the box but you’re missing some things for PWA, Accessibility, Best Practices, and SEO that will improve your scores (and in the process make your site much more friendly to visitors and search engines).

## Add a manifest file

Looks like you have a pretty lackluster score in the “Progressive Web App” category. Let’s address that.

But first, what exactly *are* PWAs?

They are regular websites that take advantage of modern browser functionality to augment the web experience with app-like features and benefits. Check out [Google’s overview](https://developers.google.com/web/progressive-web-apps/) of what defines a PWA experience.

Inclusion of a web app manifest is one of the three generally accepted [baseline requirements for a PWA](https://alistapart.com/article/yes-that-web-project-should-be-a-pwa#section1).

Quoting [Google](https://developers.google.com/web/fundamentals/web-app-manifest/):

> The web app manifest is a simple JSON file that tells the browser about your web application and how it should behave when ‘installed’ on the user’s mobile device or desktop.

[Gatsby’s manifest plugin](https://www.gatsbyjs.com/packages/gatsby-plugin-manifest/) configures Gatsby to create a `manifest.webmanifest` file on every site build.

### ✋ Using `gatsby-plugin-manifest`

1. Install the plugin:

```shell

npm install gatsby-plugin-manifest
```

1. Add a favicon for your app under `src/images/icon.png`. For the purposes of this tutorial you can use [this example icon](https://raw.githubusercontent.com/gatsbyjs/gatsby/master/docs/docs/tutorial/part-eight/icon.png), should you not have one available. The icon is necessary to build all images for the manifest. For more information, look at the docs for [`gatsby-plugin-manifest`](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-plugin-manifest/README.md).
2. Add the plugin to the `plugins` array in your `gatsby-config.js` file.

gatsby-config.js

```javascript
Copygatsby-config.js: copy code to clipboard
{
  plugins: [
    {
      resolve: `gatsby-plugin-manifest`,
      options: {
        name: `GatsbyJS`,
        short_name: `GatsbyJS`,
        start_url: `/`,
        background_color: `#6b37bf`,
        theme_color: `#6b37bf`,
        // Enables "Add to Homescreen" prompt and disables browser UI (including back button)
        // see https://developers.google.com/web/fundamentals/web-app-manifest/#display
        display: `standalone`,
        icon: `src/images/icon.png`, // This path is relative to the root of the site.
      },
    },
  ]
}
```

That’s all you need to get started with adding a web manifest to a Gatsby site. The example given reflects a base configuration — Check out the [plugin reference](https://www.gatsbyjs.com/packages/gatsby-plugin-manifest/?=gatsby-plugin-manifest#automatic-mode) for more options.

## Add offline support

Another requirement for a website to qualify as a PWA is the use of a [service worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API). A service worker runs in the background, deciding to serve network or cached content based on connectivity, allowing for a seamless, managed offline experience.

[Gatsby’s offline plugin](https://www.gatsbyjs.com/packages/gatsby-plugin-offline/) makes a Gatsby site work offline and more resistant to bad network conditions by creating a service worker for your site.

### ✋ Using `gatsby-plugin-offline`

1. Install the plugin:

```shell

npm install gatsby-plugin-offline
```

1. Add the plugin to the `plugins` array in your `gatsby-config.js` file.

gatsby-config.js

```javascript
Copygatsby-config.js: copy code to clipboard
{
  plugins: [
    {
      resolve: `gatsby-plugin-manifest`,
      options: {
        name: `GatsbyJS`,
        short_name: `GatsbyJS`,
        start_url: `/`,
        background_color: `#6b37bf`,
        theme_color: `#6b37bf`,
        // Enables "Add to Homescreen" prompt and disables browser UI (including back button)
        // see https://developers.google.com/web/fundamentals/web-app-manifest/#display
        display: `standalone`,
        icon: `src/images/icon.png`, // This path is relative to the root of the site.
      },
    },
    `gatsby-plugin-offline`,
  ]
}
```

That’s all you need to get started with service workers with Gatsby.

> 💡 The offline plugin should be listed *after* the manifest plugin so that the offline plugin can cache the created `manifest.webmanifest`.

## Add page metadata

Adding metadata to pages (such as a title or description) is key in helping search engines like Google understand your content and decide when to surface it in search results.

[React Helmet](https://github.com/nfl/react-helmet) is a package that provides a React component interface for you to manage your [document head](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/head).

Gatsby’s [react helmet plugin](https://www.gatsbyjs.com/packages/gatsby-plugin-react-helmet/) provides drop-in support for server rendering data added with React Helmet. Using the plugin, attributes you add to React Helmet will be added to the static HTML pages that Gatsby builds.

### ✋ Using `React Helmet` and `gatsby-plugin-react-helmet`

1. Install both packages:

```shell

npm install gatsby-plugin-react-helmet react-helmet
```

1. Make sure you have a `description` and an `author` configured inside your `siteMetadata` object. Also, add the `gatsby-plugin-react-helmet` plugin to the `plugins` array in your `gatsby-config.js` file.

gatsby-config.js

```javascript
Copygatsby-config.js: copy code to clipboard
module.exports = {
  siteMetadata: {
    title: `Pandas Eating Lots`,
    description: `A simple description about pandas eating lots...`,
    author: `gatsbyjs`,
  },
  plugins: [
    {
      resolve: `gatsby-plugin-manifest`,
      options: {
        name: `GatsbyJS`,
        short_name: `GatsbyJS`,
        start_url: `/`,
        background_color: `#6b37bf`,
        theme_color: `#6b37bf`,
        // Enables "Add to Homescreen" prompt and disables browser UI (including back button)
        // see https://developers.google.com/web/fundamentals/web-app-manifest/#display
        display: `standalone`,
        icon: `src/images/icon.png`, // This path is relative to the root of the site.
      },
    },
    `gatsby-plugin-offline`,
    `gatsby-plugin-react-helmet`,
  ],
}
```

1. In the `src/components` directory, create a file called `seo.js` and add the following:

src/components/seo.js

```jsx
Copysrc/components/seo.js: copy code to clipboard
import React from "react"
import PropTypes from "prop-types"
import { Helmet } from "react-helmet"
import { useStaticQuery, graphql } from "gatsby"

function SEO({ description, lang, meta, title }) {
  const { site } = useStaticQuery(
    graphql`
      query {
        site {
          siteMetadata {
            title
            description
            author
          }
        }
      }
    `
  )

  const metaDescription = description || site.siteMetadata.description

  return (
    <Helmet
      htmlAttributes={{
        lang,
      }}
      title={title}
      titleTemplate={`%s | ${site.siteMetadata.title}`}
      meta={[
        {
          name: `description`,
          content: metaDescription,
        },
        {
          property: `og:title`,
          content: title,
        },
        {
          property: `og:description`,
          content: metaDescription,
        },
        {
          property: `og:type`,
          content: `website`,
        },
        {
          name: `twitter:card`,
          content: `summary`,
        },
        {
          name: `twitter:creator`,
          content: site.siteMetadata.author,
        },
        {
          name: `twitter:title`,
          content: title,
        },
        {
          name: `twitter:description`,
          content: metaDescription,
        },
      ].concat(meta)}
    />
  )
}

SEO.defaultProps = {
  lang: `en`,
  meta: [],
  description: ``,
}

SEO.propTypes = {
  description: PropTypes.string,
  lang: PropTypes.string,
  meta: PropTypes.arrayOf(PropTypes.object),
  title: PropTypes.string.isRequired,
}

export default SEO
```

The above code sets up defaults for your most common metadata tags and provides you an `<SEO>` component to work within the rest of your project. Pretty cool, right?

1. Now, you can use the `<SEO>` component in your templates and pages and pass props to it. For example, add it to your `blog-post.js` template like so:

src/templates/blog-post.js

```jsx
Copysrc/templates/blog-post.js: copy code to clipboard
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"
import SEO from "../components/seo"

export default function BlogPost({ data }) {
  const post = data.markdownRemark
  return (
    <Layout>
      <SEO title={post.frontmatter.title} description={post.excerpt} />
      <div>
        <h1>{post.frontmatter.title}</h1>
        <div dangerouslySetInnerHTML={{ __html: post.html }} />
      </div>
    </Layout>
  )
}

export const query = graphql`
  query($slug: String!) {
    markdownRemark(fields: { slug: { eq: $slug } }) {
      html
      frontmatter {
        title
      }
      excerpt
    }
  }
`
```

The above example is based off the [Gatsby Starter Blog](https://www.gatsbyjs.com/starters/gatsbyjs/gatsby-starter-blog/). By passing props to the `<SEO>` component, you can dynamically change the metadata for a post. In this case, the blog post `title` and `excerpt` (if it exists in the blog post markdown file) will be used instead of the default `siteMetadata` properties in your `gatsby-config.js` file.

Now, if you run the Lighthouse audit again as laid out above, you should get close to—if not a perfect— 100 score!

> 💡 For further reading and examples, check out [Adding an SEO Component](https://www.gatsbyjs.com/docs/add-seo-component/) and the [React Helmet docs](https://github.com/nfl/react-helmet#example)!

## Keep making it better

In this section, we’ve shown you a few Gatsby-specific tools to improve your site’s performance and prepare to go live.

Lighthouse is a great tool for site improvements and learning — Continue looking through the detailed feedback it provides and keep making your site better!

## Next Steps

### Official Documentation

- [Official Documentation](https://www.gatsbyjs.com/docs/): View our Official Documentation for step-by-step [How-To Guides](https://www.gatsbyjs.com/docs/how-to/), big-picture [Conceptual Guides](https://www.gatsbyjs.com/docs/conceptual), and technical [Reference Guides](https://www.gatsbyjs.com/docs/reference).

### Official Plugins

- [Official Plugins](https://github.com/gatsbyjs/gatsby/tree/master/packages): The complete list of all the Official Plugins maintained by Gatsby.

### Official Starters

1. [Gatsby’s Default Starter](https://github.com/gatsbyjs/gatsby-starter-default): Kick off your project with this default boilerplate. This barebones starter ships with the main Gatsby configuration files you might need. *[working example](https://gatsbyjs.github.io/gatsby-starter-default/)*
2. [Gatsby’s Blog Starter](https://github.com/gatsbyjs/gatsby-starter-blog): Gatsby starter for creating an awesome and blazing-fast blog. *[working example](https://gatsbyjs.github.io/gatsby-starter-blog/)*
3. [Gatsby’s Hello-World Starter](https://github.com/gatsbyjs/gatsby-starter-hello-world): Gatsby Starter with the bare essentials needed for a Gatsby site. *[working example](https://gatsby-starter-hello-world-demo.netlify.app/)*

## That’s all, folks

Well, not quite; just for this tutorial. There are additional [How-To Guides](https://www.gatsbyjs.com/docs/how-to/) to check out for more guided use cases.

This is just the beginning. Keep going!

- Did you build something cool? Share it on Twitter, tag [#buildwithgatsby](https://twitter.com/search?q=%23buildwithgatsby), and [@mention us](https://twitter.com/gatsbyjs)!
- Did you write a cool blog post about what you learned? Share that, too!
- Contribute! Take a stroll through [open issues](https://github.com/gatsbyjs/gatsby/issues?q=is%3Aissue+is%3Aopen+label%3A"help+wanted") on the gatsby repo and [become a contributor](https://www.gatsbyjs.com/contributing/how-to-contribute/).

Check out the [“how to contribute”](https://www.gatsbyjs.com/contributing/how-to-contribute/) docs for even more ideas.

We can’t wait to see what you do 😄.



> Gatsby Tutorial：[https://www.gatsbyjs.com/docs/tutorial/part-eight/](https://www.gatsbyjs.com/docs/tutorial/part-eight/)