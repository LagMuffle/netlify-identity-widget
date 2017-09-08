# Netlify Identity Widget

A component used to authenticate with Netlify's Identity API. [Live demo](https://identity.netlify.com)

For a lower level library to the underlying `GoTrue` API, see [gotrue-js](https://github.com/netlify/gotrue-js).

## Usage

Simply include the widget on your site, and things like invites, confirmation codes, etc, will start working.

You can add controls for the widget with HTML:

```html
<!DOCTYPE html>
<html>
<head>
  <title>A static website</title>

  <!-- include the widget -->
  <script defer type="text/javascript" src="https://identity.netlify.com/v1/netlify-identity-widget.js"></script>
</head>
<body>
  <!-- Add a menu:
   Log in / Sign up - when the user is not logged in
   Username / Log out - when the user is logged in
  -->
  <div data-netlify-identity-menu></div>

  <!-- Add a simpler button:
    Simple button that will open the modal.
  -->
  <div data-netlify-identity-button>Login with Netlify Identity</div>
</body>
</html>
```

The widget will automatically attach itself to the window object as `window.netlifyIdentity`.

You can use this global object like this:

```js
 // open the modal
netlifyIdentity.open()

// Get the current user:
const user = netlifyIdentity.currentUser();

// Bind to events
netlifyIdentity.on('init', user => console.log(user))
netlifyIdentity.on('login', user => console.log(user))
netlifyIdentity.on('logout', () => console.log("Logged out"))
netlifyIdentity.on('error', err => console.error("Logged out"))
netlifyIdentity.on('open', () => console.log("Widget opened"))
netlifyIdentity.on('close', () => console.log("Widget closed"))

// Close the modal
loginModal.close()

// Logout the user
loginModal.logout();
```

### Module API

Netlify Identity Widget also has a [module api](https://www.npmjs.com/package/netlify-identity-widget):

```
yarn add netlify-identity-widget
```

Import or require as usual:

```js
import NetlifyIdentity from "netlify-identity-widget"
// or
const netlifyIdentity = require("netlify-identity-widget");

netlifyIdentity.init({
  container: "#netlify-modal" // defaults to document.body
});

identity.open() // open the modal

identity.on('init', user => console.log(user))
identity.on('login', login => console.log(user))
identity.on('logout', () => console.log("Logged out"))
identity.on('error', err => console.error("Logged out"))
identity.on('open', () => console.log("Widget opened"))
identity.on('close', () => console.log("Widget closed"))

// Close the modal
identity.close()

// Logout the user
loginModal.logout();

// Access the underlying gotrue instance.
// Note that doing things directly through gotrue brings a risk of getting out of
// sync between your state and the widgets state.
identity.gotrue
```

## Localhost

When using the widget on localhost, it will prompt for your Netlify SiteURL the first time it is opened.

This allows the widget to know which instance of Netlify Identity it should communicate with with zero
configuration.
