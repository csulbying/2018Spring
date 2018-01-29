# Bootstrap Tutorial

## Link Bootstrap Styles

Create a `basic.html` file in your source code folder with a body of `<h1>Bootstrap Basics</h1>`. Open it in your Chrome browser.

Go to [getbootstrap.com](getbootstrap) to downloand bootstrap. There are two ways to use bootstrap.

One is to download it and unzip the file. Inside the css folder, there is a `bootstrap.css` file. Others are custom themes or minified files. The `bootstrap.css` is just a set of css styles. Copy the file to your source code folder. Add `<link rel="stylesheet" href="bootstrap.css">` to the html head, you can see the change of you html file.

Another option is to use BootstrapCDN, copy the the CSS only link in the [getbootstrap](getbootstrap) website or the [Bootstrap document](bootstrap-doc) to your html head section. It is something like `<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">`. Comment out the previous link and bootstrap sitll works.

## Use Buttons

To use button style, add a `btn` class and a button type class. The button type could be `btn-default`, `btn-primary`, and etc. Buttons can be of different sizes. Check [bootstrap button](https://getbootstrap.com/docs/4.0/components/buttons/) for details.

Button styles can be applied to a `a`, `button`, and `input` elments. Add the following contents: 

```html
<button class="btn btn-success btn-xs">CLICK ME!</button>
<a href="http://www.getbootstrap.com" class="btn btn-info btn-lg">Bootstrap doc</a>
```

Buttons can have an active state and can be disabled. Add two more buttons.

```html
<button class="btn btn-success btn-xs active">CLICK ME!</button>
<button class="btn btn-success btn-xs" disabled="disabled">CLICK ME!</button>
```

You can customize a button color using a style like `.btn-danger { color: orange; }`. Try it in an embedded or inline style.

## Jumbotron

According to [jumbotron doc](http://getbootstrap.com/docs/4.0/components/jumbotron/), jumbotron is a lightweight, flexible component for showcasing hero unit style content.

Add the following code to your html file:

```html
<div class="jumbotron">
    <h1>This is a jumbotron</h1>
    <p>This is a simple hero unit, a simple 
        jumbotron-style component for calling extra 
        attention to featured content or information.</p>
    <button class="btn btn-success btn-lg">Hi there</button>
</div>
```

## Container

Containers are the most basic layout element in Bootstrap. They brings default grid layout systme.

[getbootstrap]: https://getbootstrap.com/
[bootstrap-doc]: https://getbootstrap.com/docs