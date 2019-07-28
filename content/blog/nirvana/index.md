---
title: "Nirvana"
date: "2019-07-28"
description: "Running web apps with bliss"
---

Before you read this, the context of [this post will help you not get angry at me](https://rtorr.com/on-javascript-fatigue/).

I believe modern tooling for the web is better than ever. This does not mean we don't have a lot to improve, or that we should stop thinking of new ideas.

One thing that has always been better about PHP, was running your code. You just embed some PHP in an HTML file, run a web server, and you are good to go. (I know its a bit more complicated in modern PHP stacks, but you still have this option).

We have a lot of options close to what I am about to describe, with many great people working on them.

Since the introduction of Ecmascript Modules, I have been thinking that one day we would go back to simpilar times (from the perspective of just messing around with code). We have, but there is still room to improve.

## Bliss

Imagine we need to serve a directory like.

```bash
.
├── index.html
└── index.js
```

This is simple enough, we have the tools. Stick with me.

Imagine we have a webserver installed called `@rtorr/nirvana`, and we use it to serve this directory.

```bash
@rtorr/nirvana ./
```

Now imagine if this web server could understand when you request `react` from code like

```javascript
import React from "react"
import ReactDOM from "react-dom"

function Main() {
  return <p>Hello world</p>
}

ReactDOM.render(<Main />, document.getElementById("main"))
```

it would understand that `react` is a package some where, in this case npm.

This is a nuanced, but an important point. There is just too much written JavaScript out there on the web that is written this way. To refactor all of our apps, and dependencies to instead use a url, like

```javascript
import React from "https://unpkg.com/react@16.7.0/umd/react.production.min.js"
import ReactDOM from "https://unpkg.com/react-dom@16.7.0/umd/react-dom.production.min.js"

function Main() {
  return React.createElement("p", null, "Hello world")
}

ReactDOM.render(
  React.createElement(Main, null),
  document.getElementById("main")
)
```

, is nearly an impossible task. This is not to mention all of the written documentation.

We should be able to copy and pase

```javascript
import React from "react"
import ReactDOM from "react-dom"

function Main() {
  return <p>Hello world</p>
}

ReactDOM.render(<Main />, document.getElementById("main"))
```

into a JavaScript file, and have our server know what to do with it.

## Challenge

[Make this work](https://github.com/rtorr/nirvana)
