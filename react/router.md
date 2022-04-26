---
title: React - Router
description: 
published: true
date: 2022-04-04T17:03:56.138Z
tags: 
editor: markdown
dateCreated: 2022-04-04T17:03:54.873Z
---

# React Router

## Main Router logic

Create a folder `/routers` containing all the files for the router logic.

First of all, create a file with the main router of the app called `AppRouter.js`.

- The `<Router>` contain all the logic of routes containing all the `<Route>` components.

- The `<Route>` is the route that loads when there is a match with the url.

```jsx
import { BrowserRouter as Router, Route } from "react-router-dom";
// here the imports to: AboutPage, ContactPage, HomePage...

const AppRouter = () => {
  return (
    <Router>
      <Route exact path="/about" component={AboutPage} />
      <Route exact path="/contact" component={ContactPage} />
      <Route exact path="/" component={HomePage} />
      <!-- more routes -->
    </Router>
  );
}

export default AppRouter;
```

Then add the component to the `App.js`.

```jsx
import React from "react";
import AppRouter from "./routers/AppRouter";

const App = () => {
  return (
    <div>
      <AppRouter />
    </div>
  );
}

export default App;
```

## Switch

The `<Switch>` component wrap the routes and prevent to match when the path contains the first characters on the route. It loads only the first match in the code.

Without that, if you write `/contact` it matchs with `/`, and `/contact`.

```jsx
<Router>
  <Switch>
    <Route exact path="/about" component={AboutPage} />
    <Route exact path="/contact" component={ContactPage} />
    <Route exact path="/" component={HomePage} />
    <!-- more routes -->
  </Switch>
</Router>
```

## Route

The route component load the component when the url match with the path value.

- The path attribute is the url that loads the component when matched.
- The `exact` atribute prevent to match with more routes. It loads only with the *exact* url in the path.
- Is possible to load a component with the attribute or even wrap the children elements.

```jsx
<Route exact path="/home" >
  <HomePage/>
</Route>

<!-- short form -->
<Route exact path="/contact" component={ContactPage} />
```

### Route with parameters with useParams

In a route is possible to get a parameter from the URL addign to the path `/:parameter`.

```jsx
<Route exact path="/profile/:username" component={ProfilePage} />
```

The component can get the value of the parameter with the `useParams` hook.

```jsx
import React from "react";
import { useParams } from "react-router-dom";

const ProfilePage = () => {
  const { username } = useParams();

  return (
    <div>
      <h1>Hi {username}!</h1>
    </div>
  );
}

export default ProfilePage;
```

### 404 Page redirection

With the path `*` and the `<Redirect>` is possible to filter all the wrong routes and reditect to a 404 page component.

```jsx
<!-- all routes -->
<Route path="/404" component={NotFoundPage} />
<Route path="*">
  <Redirect to="/404" />
</Route>
```

## NavLink

React links are similar to HTML links but they don't reload the webstie, they only reload the router components.

- The `activeClassName` property allow to assign a css property to the active link.
- The `exact` property has the same funtionality as in the `Route`.

```jsx
<ul>
  <li>
    <NavLink exact to="/" activeClassName="active">
      Home
    </NavLink>
  </li>
  <li>
    <NavLink exact to="/about" activeClassName="active">
      About
    </NavLink>
  </li>
</ul>
```