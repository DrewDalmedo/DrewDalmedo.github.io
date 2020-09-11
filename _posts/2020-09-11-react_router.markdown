---
layout: post
title:      "React Router"
date:       2020-09-11 17:39:37 +0000
permalink:  react_router
---


**What is React Router?**

While I was learning React at Flatiron, our class was introduced to the idea of “client-side routing.” The concept itself was simple: why rely on the backend to display data when that should be the frontend’s job? When we implement client-side routing, not only do we gain additional organization and clarity when working with the frontend, but we also gain a ton of speed and save the user valuable time.

When you use client-side routing with React and React Router, you’re effectively creating a SPA (Single Page Application), but rather than rendering all of your components all at once, you’re rendering them individually and swapping them out with other components when they are no longer needed. This is the reason for the increased speed, but at the cost of longer initial loading times, as everything (page content, styling, etc) is being loaded. 


**Quick Start**

To get started with React Router, you first need to install it as a project dependency. Open a terminal and run the following command in your project’s directory:

	
```
npm install -S react-router-dom
```

For those unfamiliar, the -S flag signals npm to save the new package we just installed (react-router-dom) to package.json, ensuring that anyone else who wants to contribute to the project will have the required dependency when they run ```npm install```.

After you’ve installed React Router, open up App.js and rewrite the file like this:


```
import React from 'react';

const App = props => {
  return (
    <div>
      Hello, world!
    </div>
  )
}

export default App;
```

Great! We’ve got a blank slate to work with. Let’s create a couple of stateless components for us to use as examples:


```
import React from 'react';

const Home = props => {
  return (
    <div>
      Home sweet home!
    </div>
  )
}

const About = props => {
  return (
    <div>
      This project demonstrates React Router.
    </div>
  )
}

const App = props => {
  return (
    <div>
      Hello, world!
    </div>
  )
}

export default App;
```

NOTE: Normally you’d separate these stateless components into different files (such as Home.js and About.js), but for the sake of simplicity and clarity I’ve put them all in App.js

Now that we’ve got 3 example components, let’s get started with implementing React Router. The “meat and potatoes” of React Router are these two components: <BrowserRouter>, and <Route>. Without these, React Router simply wouldn’t work. Let’s import them now:

```
import React from 'react';
import { BrowserRouter, Route } from 'react-router-dom'

const Home = props => {
  return (
    <div>
      Home sweet home!
    </div>
  )
}

const About = props => {
  return (
    <div>
      This project demonstrates React Router.
    </div>
  )
}

const App = props => {
  return (
    <div>
      Hello, world!
    </div>
  )
}

export default App;
```

To implement these newly imported components, let’s go back down to our App function and replace the div with a BrowserRouter:

```
const App = props => {
  return (
    <BrowserRouter>
      {/* we'll implement Routes here! */}
    </BrowserRouter> 
  )
}
```

BrowserRouter, according to the documentation, is “A Router that uses the HTML5 history API to keep your UI in sync with the URL.” In simpler terms, it uses features built into your browser itself to manage what content is being displayed at a given URL. There are different kinds of higher level routers like BrowserRouter, such as HashRouter, MemoryRouter, and NativeRouter, but in this guide we’ll just stick with BrowserRouter.

Now, let’s add in some actual routes, shall we?


```
const App = props => {
  return (
    <BrowserRouter>
      <Route path="/" />
      <Route path="/about" />
    </BrowserRouter> 
  )
}
```

Great! We have the routes built out for our pages, but if you try to actually visit them, you’ll be greeted with a completely blank page. What gives?

When we create routes, we need to pass in what we want to render as a prop. There are a few ways to do this: we can use the render prop, the component prop, or the children prop. Since we already have our components defined, let’s render the pages using the component prop.


```
const App = props => {
  return (
    <BrowserRouter>
      <Route path="/" component={Home} />
      <Route path="/about" component={About} />
    </BrowserRouter> 
  )
}
```

Awesome! When we first load our app, everything seems to be working perfectly. However, go and try to navigate to the /about route. Now we can see both the home component’s text and the about component’s text, which wasn’t what we had intended to do at all!
This is because the two routes, “/” and “/about”, technically match, and we’re now rendering two components per page instead of one. In order to fix this, we need to implement a whole other component from React Router: switches.

Let’s go back to our import and add the following:

```
import { BrowserRouter, Route, Switch } from 'react-router-dom'
```

Now, let’s go back down to our App function and nest all the routes we just wrote inside of a <Switch>


```
const App = props => {
  return (
    <BrowserRouter>
      <Switch>
        <Route path="/" component={Home} />
        <Route path="/about" component={About} />
      </Switch>
    </BrowserRouter> 
  )
}
```

Great, now we’ve got components rendering one at a time rather than all at once. However, now we’ve got another bug: the Home component still renders on the about page, and this time, it’s the only component there!

The reason why this is happening is because the home component is being rendered at the root of the route ("/”). To make sure that the component only renders at the appropriate path, we need to add an extra prop: exact.


```
<Route exact path="/" component={Home} />
```

Let’s check out our app again, and poof! Everything works as intended.

Now that we’ve got the routes up and working, let’s add in some links so that users can visit them without typing them in manually into the address bar. First, let’s import another component from React Router: Link.


```
import { BrowserRouter, Route, Switch, Link } from 'react-router-dom'
```

Awesome. Now, let’s go back to our App function and add in some links:

```
const App = props => {
  return (
    <BrowserRouter>

      <Switch>
        <Route exact path="/" component={Home} />
        <Route path="/about" component={About} />
      </Switch>

      <div>
        <Link to="/">Home</Link>
      </div>
      <div>
        <Link to="/about">About</Link>
      </div>

    </BrowserRouter> 
  )
}
```

Now, whenever we try clicking on one of the links, we’ll be brought to the appropriate page, without having to load it from scratch!
