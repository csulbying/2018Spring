# Course Setup

A professional web developer uses many tools to improve productivity and software quality. An essential set of tools used in this course are:

* Node.js: the platform to serve our web site.
* Visual Studio Code (VS Code): the IDE to edit/run/debug code.
* Git: the software version management tool.
* Heroku: the cloud application host service.

We use VS Code to write/run/debug Node.js + Express.js code locally. Then push code to Github. Deploy code to Heroku thus the application can be accessible to the public.

## Node.js

Node.js is a JavaScript runtime platform that is used to JavaScript applications. Go to [https://nodejs.org](https://nodejs.org) to download and install the latest (current) Node.js.

There are two stable versions listed in the above page: a long term support (LTS) version and the current version. For learning purpose, just download the latest version. For production deployment, you may want to use a LTS version.

Node.js comes with a package management tool named "npm". npm is used to install node.js packages such as Express.js and many others.

Once you install it, run `node --version` to make sure it is installed correctly.

## VS Code

VS Code is a free, open source, simple, and powerful Integrated Development Environment (IDE) for web application development. It has many plugins that provide many functions in addition to its core  features. It has built-in support for Git.

Go to [https://code.visualstudio.com/download](https://code.visualstudio.com/download) to download it for your operating systems.

## Git and GitHub

Git is the most popular software version management tool. VS Code has built-in support for Git therefore we only need to use it for project initial setup.

Go to [https://git-scm.com/downloads](https://git-scm.com/downloads) to download and install the latest version of Git. run `git --version` to verify the installation.

In Git terms, a software project is called a repository. GitHub is a cloud service that hosts Git repositories.

Go to [https://github.com](https://github.com) to create an account if you don't have one.

To link the local Git with your GitHub account and not type username and password repetitively, you need to use a credential helper to cache GitHub username and password. For Mac OS, check [this article](https://help.github.com/articles/caching-your-github-password-in-git/#platform-mac). For Windows, check [this article](https://help.github.com/articles/caching-your-github-password-in-git/#platform-windows).