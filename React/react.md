# React

React is a JavaScript library that provides the View layer for the MVC model (Model-View-Controller).

## Basics

## Components

A React app is made of components. Each component will be an element or group of elements in a website.
For example, a search bar, video, buttons, etc.

React renders (loads to the DOM) many components into a website at the same time with an amazing speed.

Components can be nested and put aside of each others. For example, a list could be a component, with each element of said list being another component.
We should also have a big, final component that wraps the whole applications.

This structure promotes **code reusability**.

_Note:_ A golden rule is that we make a **file per component**, no matter how small.

To create a component, we will do it as:

```JSX
const App = () => {
  return <div> Hi! </div>; // This line is doing a React.createElement() under the hood
};
```

where `<div>Hi!</div>;` is using the JSX syntax to add html to the JavaScript.

---

JSX is a preprocessor step or phase that is inchage of adding XML syntax to JavaScript.
It's similar in to XML in that it has tags, attributes, children, etc.

---

In the case showed above, we are just creating a div element, with a String "Hi!" element on it. Easy.
But if we wanted to add some more, we'll wrap it all in parentheses, in the form:

```JSX
const App = () => {
    return (
        <div>
            <SearchBar/>
            // Where SearchBar is the given variable name of an imported component
        </div>
    );
}
```

We will create a "components" folder, usually inside the "src" folder, with the said files inside.

![Components Structure](/img/components-structure.png)

### Exporting modules

Each of this files must **import** React at the beginning of the document and export the component at the end.

```javascript
// In search_bar.js
import React from "react";

const SearchBar = () => {
    // Code
}

export default SearchBar;
```

We should import the components into the main file, or index.js in this case, obviously.

```javascript
// In index.js
import React from "react";
import ReactDOM from "react-dom";

import SearchBar from "./components/search_bar";
// ...
```

### Classes

There's two types of components in React:

- Functional components
- Class components

---

**Functional component:** It's just a function that does things and returns something.

```JSX
// Functional Component
const Div = () => {
    return <div>Not-complicated</div>
};
```

---

**Class component:** It's a component that has an internal record keeping. Some ability of being aware of himself and what happens to him after it renders.

Class components make use of the ES6 syntax. Classes in JavaScript are objects.

When we define a class component, we still have to give it the ability to render itself / return some JSX.

Every class component in React must have a render method.

```JSX
import React from "React";

class SearchBar extends React.Component {
    render() {
        return <input />; // It must return some JSX like the functional component.
    }
}
```

Using the ES6 object destructuring, the previus code can turn into:

```JSX
import React, { Component } from "react";

class SearchBar extends Component {
    // Some Code
}
```

In general, we should try to start with functional components, and only when we need it, we should switch to class components.

### State

Handling events in React takes two steps:

- We declare an event handler. This will be a function that run when the event occurs.
- We pass the event handler to the element that we want to monitor for events.

First, we will have to declare a function in the class component. Usually, the method name will be: _onInputChange()_ or _handleInputChange()_.

```JSX
class SearchBar extends Component {
    // Mandatory render function inside a class     component
    render() {
        // onChange is a React defined property. It's watching the Change event on the input tag.
        return <input onChange = { this.onInputChange } />;
    }
    // Event handler
    onInputChange(event) {
        console.log(event.target.value);
    }
}
```