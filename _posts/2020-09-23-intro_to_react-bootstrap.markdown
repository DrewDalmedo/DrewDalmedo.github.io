---
layout: post
title:      "Intro to react-bootstrap"
date:       2020-09-23 22:57:11 +0000
permalink:  intro_to_react-bootstrap
---


Hey there! 

In my [last blog post](https://drewdalmedo.github.io/react_router), we covered the basics of react-router, a client-side routing tool built for React. In this blog, we're going to continue to improve upon our tiny little React app and add some great styling with *react-bootstrap*!

[React-bootstrap](https://react-bootstrap.github.io/) is, in essence, [Bootstrap](https://getbootstrap.com/), but rewritten to be actual React components! Using react-bootstrap over regular old bootstrap allows the JSX we write to be coherent and consistent with the rest of our app, in addition to removing the need for unnecessary dependencies such as jQuery.

**Basic Setup**

If you followed the last blog post, you're all good to go! Skip forward to "Getting Started With React-Bootstrap." If you didn't, you need to follow the instructions below.

First, open up a terminal, `cd` to the directory you want your project in, and create a blank React project with the following command:

`
npx create-react-app react-bootstrap-tutorial
`

Great! Now, `cd` into the directory and install `react-router`, which will be needed for navigating between pages:

`
npm install -S react-router
`

Awesome. Now, open your IDE or text editor of choice, navigate to the `src` directory, and open `App.js`. After you've got that done, copy the following code and replace your `App.js` with this:


```
import React from 'react';
import { BrowserRouter, Route, Switch, Link } from 'react-router-dom'

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
    <BrowserRouter>

      <Switch>
        <Route exact path="/" component={Home} />
        <Route path="/about" component={About} />
      </Switch>

      <div className="home-link">
        <Link to="/">Home</Link>
      </div>
      <div className="about-link">
        <Link to="/about">About</Link>
      </div>

    </BrowserRouter> 
  )
}


export default App;
```

Now we're all set up! Quickly run `npm start`, and watch our app come to life!

**Getting Started With React-Bootstrap**

First, let's install the required dependencies with npm:

```
npm install -S bootstrap react-bootstrap
```

In order to see any of the styling changes we're about to make, we need to import the following `css` file in `index.js`:

```
// index.js
...
import 'bootstrap/dist/css/bootstrap.min.css';
...
```

Before we get started redesigning our components, we should take note of something: all of our components are located inside of `App.js`! While this was fine for the purposes of demonstrating `react-router`, it's going to start getting really complicated and messy when we try to implement react-bootstrap into our app. So, let's refactor!

First, we'll create a new directory inside of our `src` folder, called `components`. After we've got that done, open up our new directory and create two new files: `Home.js` and `About.js`:

```
// About.js
import React from 'react';
```

```
// Home.js
import React from 'react';
```

Great. Now, let's take a look at our `App.js` file again:

```
// App.js
import React from 'react';
import { BrowserRouter, Route, Switch, Link } from 'react-router-dom'

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
    <BrowserRouter>

      <Switch>
        <Route exact path="/" component={Home} />
        <Route path="/about" component={About} />
      </Switch>

      <div className="home-link">
        <Link to="/">Home</Link>
      </div>
      <div className="about-link">
        <Link to="/about">About</Link>
      </div>

    </BrowserRouter> 
  )
}

export default App;
```

Let's move our stateless components to the correct files. First, let's move our Home component over:

```
// Home.js
import React from 'react';

const Home = props => {
  return (
    <div>
      Home sweet home!
    </div>
  )
}

export default Home;
```

```
// App.js
const About = props => {
  return (
    <div>
      This project demonstrates React Router.
    </div>
  )
}

const App = props => {
  return (
    <BrowserRouter>

      <Switch>
        <Route exact path="/" component={Home} />
        <Route path="/about" component={About} />
      </Switch>

      <div className="home-link">
        <Link to="/">Home</Link>
      </div>
      <div className="about-link">
        <Link to="/about">About</Link>
      </div>

    </BrowserRouter> 
  )
}
```

And now do the same for our About component:

```
// About.js
import React from 'react';

const About = props => {
  return (
    <div>
      This project demonstrates React Router.
    </div>
  )
}

export default About;
```

```
// App.js
const App = props => {
  return (
    <BrowserRouter>

      <Switch>
        <Route exact path="/" component={Home} />
        <Route path="/about" component={About} />
      </Switch>

      <div className="home-link">
        <Link to="/">Home</Link>
      </div>
      <div className="about-link">
        <Link to="/about">About</Link>
      </div>

    </BrowserRouter> 
  )
}
```

Awesome! The last thing we need to do is import the components from our new files so that `App.js` can see them.

```
// App.js
import React from 'react';
import { BrowserRouter, Route, Switch, Link } from 'react-router-dom'

// our refactored components
import Home from './components/Home'
import About from './components/About'

const App = props => {
  return (
    <BrowserRouter>

      <Switch>
        <Route exact path="/" component={Home} />
        <Route path="/about" component={About} />
      </Switch>

      <div className="home-link">
        <Link to="/">Home</Link>
      </div>
      <div className="about-link">
        <Link to="/about">About</Link>
      </div>

    </BrowserRouter> 
  )
}

export default App;
```

Great! Now, let's get started with styling our web app.

**The Building Blocks of React-Bootstrap**

The magic behind bootstrap and react-bootstrap is it's grid system. Without this, it wouldn't be able to rescale our page's elements appropriately to our device or display size! 

Let's take another look at our Home component:

```
// Home.js
import React from 'react';

const Home = props => {
  return (
    <div>
      Home sweet home!
    </div>
  )
}

export default Home;
```

We're now going to import a couple components from react-bootstrap: `Container`, `Row`, and `Col`. 

```
// Home.js
import React from 'react';
// react-bootstrap components
import { Container, Row, Col } from 'react-bootstrap'

const Home = props => {
  return (
    <div>
      Home sweet home!
    </div>
  )
}

export default Home;
```

If you're familiar with bootstrap, you'll recognize these as the class names you'd use for divs! In react-bootstrap, these were formalized as actual components you can render with JSX.

Next, in our stateless component, let's replace our `<div>` with a `<Container>`:

```
const Home = props => {
  return (
    <Container>
      Home sweet home!
    </Container>
  )
}
```

When your page refreshes after you save, you can begin to see our styling changes take shape! Instead of our text, "Home sweet home!" being aligned to the left, it's aligned a little bit more towards the center then it was before. However, it's still *technically* aligned to the left! The only thing that's really changed is the *padding* on the sides.

We'll get to our text later. For now, let's focus on our `<Container>` component. There's only one essential prop we can pass to our `<Container>` component: `fluid`. This prop determines the width of our container across devices! 

The default value of the prop, without it being passed in, is false, meaning our default `<Container>` components will maintain their default padding across most devices.

For the sake of our styling, let's set our container to be fluid, so that it consistently fills up the width of our screen:

```
const Home = props => {
  return (
	  <Container fluid>
		  Home sweet home!
		</Container>
	)
}
```

Now that we've got our container all set up, let's discuss the other two building blocks of react-bootstrap: Rows and Cols.

Rows, like their name suggests, create a new row in our Container's grid, in which we can present data in and have it be adjusted to the appropriate width for our container. Let's create a basic Row now:

```
const Home = props => {
  return (
	  <Container fluid>
		  <Row>
			  Home sweet home!
			</Row>
		</Container>
	)
}
```

Rows will span the entire width of a container, which is important to note for our next component: `Col`.

Cols help us to divide our rows into little, automatically sized bits! Let's try separating our words into three separate pieces:

```
const Home = props => {
  return (
	  <Container fluid>
		  <Row>

        <Col>
          Home 
        </Col>

        <Col>
          sweet 
        </Col>

        <Col>
          home!
        </Col>

			</Row>
		</Container>
	)
}
```

Now, when we check back on our page, we can see our little greeting separated into three columns!

This design, while entirely functional, looks a little... dull, doesn't it? Let's try spicing it up a bit!

First, let's go back up to our `<Container>` component and add in the following class name:

```
<Container fluid className="text-center">
  ...
</Container>
```

When we check back up on our web page, all of our text should be centered within each column! Now, let's try setting the style of the container to a couple other attributes:

```
<Container
  fluid
	className="text-center"
	style={{
	  backgroundColor: "black",
		color: "white",
		fontSize: "24px"
	}}
>
  ...
</Container>
```

From here on out, the sky's the limit with how you style your app! Try fooling around a bit with the `About` component, and refactor it into a component which uses `react-bootstrap`!

These were only the building blocks for how `react-bootstrap` works. There are *tons* of other components to try out, including `<Button>` components, `<Image>` components, and even `<Navbar>` components! If you want to learn more about those, head on over to the [official documentation](https://react-bootstrap.github.io/getting-started/introduction/).

Happy hacking!
