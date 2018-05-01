# Express and MongoDB CRUD Demo

## 1 Initial Setup

This tutorial shows how to create an express web app that has CRUD operations.

First, install `express-generator` command line to initialize a project.

`npm install -g express-generator`
`express crud-demo --view=ejs`

It creates a project in `crud-demo` folder. Inside the `crud-demo` folder, run `npm install` to install required packages. You can run `npm start` and see the initial web site.

Second, create a MongoDB account in `mlib.com`. The accounts has 500MB free space. Click `Create new` to create a new database with the free `SANDBOX` plan type. Give it a name such as `is445`. Then create a database user by clicking `Users` tab. The page shows the connections string like `mongodb://<dbuser>:<dbpassword>@ds163689.mlab.com:63689/is445`.

Then install `mongoose` database driver: `npm install -S mongoose`.

Then add the following code, right before the last line of `module.exports = app;`, to `app.js`:

```js
const mongoose = require("mongoose");

const user = process.env.MDB_USER;
const passwd = process.env.MDB_PASSWORD;

mongoose
  .connect(`mongodb://${user}:${passwd}@ds163689.mlab.com:63689/is445`)
  .then(() => console.log("connection successful"))
  .catch(err => console.error(err));
```

You should set enviornment variables `MDB_USER` and `MDB_PASSWORD` to use your MongoDB user account and password. To avoid setting in devolopment, you can use dotenv package by using `npm i -S dotenv` and create a `.evn` file in project root folder with the following content:

```sh
MDB_USER=your-mongodb-user
MDB_PASSWORD=your-mongodb-password
```

Add the following lines to the begenning of `app.js`

```javascript
// load env
if (process.env.NODE_ENV !== "production") {
  require("dotenv").load();
}
```

Finally, install `nodemon` using `npm install -g nodemon` and run it:
`nodemon`. You should see the output `connection sucessful`. Congratulations, you successfully connented to MongoDb.

## 2 Change Home Page

Change the `routers/index.js` to have the following code:

```js
router.get("/", function(req, res, next) {
  res.render("index", { title: "IS445 Demo" });
});
```

Add the following content to `views/index.ejs`:

```html
<p>Here is the link to
  <a href="users">users</a>
</p>
```

It is just a link to `/users`.

## 3 Create Mogoose Model

Create a `models` folder and create a `users.js` file in it.

```js
const mongoose = require("mongoose");

const UserSchema = new mongoose.Schema({
  name: String,
  address: String,
  position: String,
  salary: Number,
  updated_at: { type: Date, default: Date.now }
});

module.exports = mongoose.model("User", UserSchema);
```

A mongoose model defines the schema of a collection. A collection is a set of records in MongoDb.

## 4 List Users

### 4.1 Create a Controller

Create a user controller file `controllers/user.js` as the following:

```js
const mongoose = require("mongoose");
const User = require("../models/user");

const userController = {};

user.list = function(req, res) {
  User.find({}).exec(function(err, users) {
    if (err) {
      console.log("Error:", err);
    } else {
      res.render("../views/users/index", { users });
    }
  });
};

module.exports = userController;
```

The controller list function finds all users from the backend database and pass it to the `index` view.

### 4.2 Create a List View

Create a `views/users/index.ejs` as the following:

```html
<!DOCTYPE html>
<html>

<head>
  <title>Employee List</title>
  <link rel='stylesheet' href='/stylesheets/style.css' />
</head>

<body>
  <div class="container">
    <h3>
      <a href="/users/create">Create New User</a>
    </h3>
    <h1>User List</h1>
    <% if(users.length>0) { %>
      <table>
        <thead>
          <tr>
            <th>User Name</th>
            <th>Position</th>
            <th>Salary</th>
          </tr>
        </thead>
        <tbody>

          <% for(var i=0; i<users.length;i++) { %>
            <tr>
              <td>
                <a href="/users/show/<%= users[i]._id%>">
                  <%= users[i].name%>
                </a>
              </td>
              <td>
                <%= users[i].position%>
              </td>
              <td>
                <%= users[i].salary%>
              </td>
            </tr>
            <% } %>
        </tbody>
      </table>
      <% } else { %>
        <div>No users found.</div>
        <% } %>
  </div>
</body>

</html>
```

### 4.3 Create a Route Path

Change the `routes/users.js` to have the following content:

```js
const express = require("express");
const router = express.Router();

const user = require("../controllers/user");

// Get all users
router.get("/", user.list);

module.exports = router;
```

### 4.4 Test Run

Run the application and you should see `No users found` because there is not any users in the database.

## 5 Create a User

Create a `views/users/create.ejs` as the following:

```html
<!DOCTYPE html>
<html>

<head>
  <title>Create a User</title>
  <link rel='stylesheet' href='/stylesheets/style.css' />
</head>

<body>
  <div class="container">
    <h3>
      <a href="/users">User List</a>
    </h3>
    <h1>Create New User</h1>
    <form action="/users/save" method="post">
      <table>
        <tbody>
          <tr>
            <td>Name</td>
            <td>
              <input type="text" name="name" />
            </td>
          </tr>
          <tr>
            <td>Address</td>
            <td>
              <textarea name="address"></textarea>
            </td>
          </tr>
          <tr>
            <td>Position</td>
            <td>
              <input type="text" name="position" />
            </td>
          </tr>
          <tr>
            <td>Salary</td>
            <td>
              <input type="number" name="salary" />
            </td>
          </tr>
          <tr>
            <td colspan="2">
              <input type="submit" value="Save" />
            </td>
          </tr>
        </tbody>
      </table>
    </form>
  </div>
</body>

</html>
```

Create two controller functions in `controllers/user.js`:

```js
userController.create = function(req, res) {
  res.render("../views/users/create");
};

userController.save = function(req, res) {
  var user = new User(req.body);

  user.save(function(err) {
    if (err) {
      console.log(err);
      res.render("../views/users/create");
    } else {
      console.log("Successfully created a user.");
      res.redirect("/users/");
    }
  });
};
```

Add the following two paths to `routes/users.js`

```js
// Create user
router.get("/create", user.create);

// Save user
router.post("/save", user.save);
```
