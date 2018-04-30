# 1 Introduction

This tutorial shows how to create an express web app that has CRUD operations.

First, install `express-generator` command line to initialize a project.

`npm install -g express-generator`
`express crud-demo --view=ejs`

It creates a project in `crud-demo` folder. Inside the `crud-demo` folder, run `npm install` to install required packages. You can run `npm start` and see the initial web site.

Second, create a MongoDB account in `mlib.com`. The accounts has 500MB free space. Click `Create new` to create a new database with the free `SANDBOX` plan type. Give it a name such as `is445`. Then create a database user by clicking `Users` tab. The page shows the connections string like `mongodb://<dbuser>:<dbpassword>@ds163689.mlab.com:63689/is445`.

Then install `mongoose` database driver: `npm install -S mongoose`.

Then add the following code to `app.js`:

```javascript
const mongoose = require("mongoose");

const user = process.env.MDB_USER;
const passwd = process.env.MDB_PASSWORD;

mongoose
  ..connect(`mongodb://${user}:${passwd}@ds163689.mlab.com:63689/is445`)
  .then(() => console.log("connection successful"))
  .catch(err => console.error(err));
```

You should change the `<dbuser>:<dbpassword>@...` to use your database user account and connection string.

Finally, install `nodemon` using `npm install -g nodemon` and run it:
`nodemon`. You should see the output `connection sucessful`.

# 2 Create Mogoose Model

Create a `models` folder.
