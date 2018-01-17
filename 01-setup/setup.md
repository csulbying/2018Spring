# Course Setup

A professional web developer uses many tools to improve productivity and software quality. An essential set of tools used in this course are:

* Node.js: the platform to serve our web site.
* Visual Studio Code (VS Code): the IDE to edit/run/debug code.
* Git: the software version management tool.
* Heroku: the cloud application host service.

We use VS Code to write/run/debug Node.js + Express.js code locally. Then push code to Github. Deploy code to Heroku thus the application can be accessible to the public.

## 1 Install Software

### 1.1 Node.js

Node.js is a JavaScript runtime platform that is used to JavaScript applications. Go to [https://nodejs.org](https://nodejs.org) to download and install the latest (current) Node.js.

There are two stable versions listed in the above page: a long term support (LTS) version and the current version. For learning purpose, just download the latest version. For production deployment, you may want to use a LTS version.

Node.js comes with a package management tool named "npm". npm is used to install node.js packages such as Express.js and many others.

Once you install it, run `node --version` to make sure it is installed correctly.

### 1.2 VS Code

VS Code is a free, open source, simple, and powerful Integrated Development Environment (IDE) for web application development. It has many plugins that provide many functions in addition to its core  features. It has built-in support for Git.

Go to [https://code.visualstudio.com/download](https://code.visualstudio.com/download) to download it for your operating systems.

### 1.3 Git and GitHub

Git is the most popular software version management tool. VS Code has built-in support for Git therefore we only need to use it for project initial setup.

Go to [https://git-scm.com/downloads](https://git-scm.com/downloads) to download and install the latest version of Git. run `git --version` to verify the installation.

In Git terms, a software project is called a repository. GitHub is a cloud service that hosts Git repositories.

Go to [https://github.com](https://github.com) to create an account if you don't have one.

Use `git config --global user.name "Mona Lisa"` to set up a global username for all your repositories. Use `$ git config --global user.email "email@example.com"` to set up an email for all your repositories.

To link the local Git with your GitHub account and not type username and password repetitively, you need to use a credential helper to cache GitHub username and password. For Mac OS, check [this article](https://help.github.com/articles/caching-your-github-password-in-git/#platform-mac). For Windows, check [this article](https://help.github.com/articles/caching-your-github-password-in-git/#platform-windows). Run `git config --global credential.helper 'cache --timeout=3600'` to let Git cache your password for 1 hour (3600 seconds). This [stackoverflow question](https://stackoverflow.com/questions/5343068/is-there-a-way-to-skip-password-typing-when-using-https-on-github#) has several answers.

## 2 The First Node.js Project

### 2.1 Create a Github Repository

Create a new repository in Github, give it a unique name such as `First-Project` and a description. By default, it is "Public" that is accessible to anyone. Check the "Initialize this repository with a README" option to let GitHub create an initial `README.md` file.

There are two buttons above the "Create repository" button. For "Add .gitignore", select the "Node". For "Add a license", select "Apache License 2.0" or any one you like. Then click the "Create repository" button to create the repository.

Then in the created repository page, click "Clone or download" button on the top right of the file list. Click the copy icon on the right to copy the "Clone with HTTPS" URL. The URL will be uased as the source of `git clone` command.

### 2.2 Clone to Local Computer

In a terminal window, go to a loca folder, type a command like `git clone https://github.com/your-name/first-project.git`. Replace `your-name` with your Github username. This will create another folder named `first-project` in the current folder. Go to the `first-project` fodler.

Then run VS code and open the `first-project` folder as the current project.

### 2.3 Node.js Initialization

 In VS Code, open a terminal by using a key combination of ``Ctrl + ` ``. The terminal opens in the `first-project` fodler, type `npm init -y` to initialize a Node.js project. The command only creates a `package.json` file that has meta-data about a Node.js project. If you don't like the VS Code termina, you can run your OS terminal program, `cmd` or `powershell` for windows and `termainl` for MacOS to preform all command line tasks. You should be in the project folder to run the command.

 In the source control icon, it shows that there is a new file `package.json` with a "U" letter on the right. The "U" means that it is a new file in "uncommitted" state. Type a short message such as "add package.json" and click the check-in icon. The source control shows a line of "CHANGES 0".

Then click the "..." icon on the top right and select "Push" to push the commit to Github repository. You can check the Github repository that there is a new commit and a new file named "package.json".

### 2.4 Install the `express` Package

In VS Code terminal window, type `npm install express` to install the `express` package. The `package.json` file has the following new lines:

```json
"dependencies": {
    "express": "^4.16.2"
}
```

It shows that the project has a dependency of the `express` package.

### 2.5 Create `server.js`

Creat a `server.js` file with the following content:

```js
const express = require('express')
const app = express()

// Serve up content from public directory
app.use(express.static(__dirname + '/website'))

const port = 3377
console.log(`Server listening at port ${port}`)
app.listen(port)
```

The code will serve static files from a `website` folder.

### 2.6 Create `index.html`

Create a new folder `website` and an `index.html` file in this new folder. It is a simple HTML file with the following content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Hello World</title>
</head>
<body>
    <h1>Hello World</h1>
</body>
</html>
```

### 7. Run the Application

In VS Code terminal, run `node server` and it should display "Server listening at port 3377". Open a browser and type `localhost:3377` in the address bar to access the HTML page.

To stop the node application, type `Ctrl + C`.

In node.js, it's common to use "npm" to run different commands. To run this application, add a new line to the "scripts" section of `package.json`. It is like the following: 

```json
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node server"
},
```

Then in VS Code command line or your OS terminal window, run `npm start` and it runs as before.