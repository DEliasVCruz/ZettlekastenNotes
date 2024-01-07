# lang.js.browser.storage.local

Store data in a client's local machine with JS from the browser

## Synopsis

```js
localStorage.setItem(<key>, <value>);
```

## Overview

The LocalStorage API gives front-end web developers access to a simple
key-value datastore that can be used to save data on a user’s computer.

The data that you add to the LocalStorage datastore is sandboxed to your
website’s domain name. This means that your web application can’t see the
data stored by any other applications and those applications cannot see
the data stored by yours.

Sub-domains are treated as separate domains and are therefore given their
own datastore.

To be safe, you should assume that your web application has only 2.5mb
of storage space

## Cookbook

### Add data to the local storage

To store data in the local storage you can use the `setItem()` function
of the `localStorage` object, that acts as key value pair

```js
localStorage.setItem("name", "Daniel Vilela");
```

You can also set values in the local storage as:

- Atribute values `localStorage.name = 'Daniel Vilea'`
- A record value `localStorage['name'] = 'Daniel Vilela'`

### Get data from local storage

You can use the `getItem()` function with the `key` that you use to
store the data

It will retrieve `undefined` or `null` if you try to access an
invalid key (one that does not exists)

```js
var name = localStorage.getItem("name");

if (name) {
  console.log(name);
}
```

### Remove data from local storage

To remove a single item use `removeItem(<key>)` function

```js
localStorage.removeItem("name");
```

### Clear the local storage datastore

To clear the whole datastore of local storage use the `clear()` function

```js
localStorage.clear();
```

### Check if the browser has support for local storage

Since this is a relatively new feature it may not work on every
browser.

Thus if you want to check for compatibility and fall back to a
different method like [cookies]() or using the server

```js
if (localStorage) {
  // Use localStorage normally
} else {
  // Use an alternative like cookies or requests
}
```
