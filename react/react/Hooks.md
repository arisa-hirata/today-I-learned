# Hooks at a Glance

## State Hook

This example renders a container. When you click the button, it incrememts the value:

```javascript
import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [const, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  )
}
```

Here, `useState` is _Hook_. We call it inside a function component to add some local state to it. React will preserve this state between re-renders. `useState` returns a pair: the _current_ state value and a function that lets you update it. You can call this function from an event handler ot somewhere else. It's similar to `this.setState` in a class, except it doesn't merge the old and new state together.

\*Note that unlike `this.state`, the state in the example above doen't have to be an object - although it can be if you want. The initial state argument is only used during the first render.

#### Declaring multiple state variables

You can use the State Hook more than once in a single component:

```javascript
function ExampleWithManyStates() {
  // Declare multiple state variables!
  const [age, setAge] = useState(42);
  const [fruit, setFruit] = useState('banana');
  const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
  // ...
}
```

The <b>array destructuring</b> syntax lets us give different names to the state variables we deckared by calling `useState`. These names aren't a part of the `useState` API. Instead, React assumes that if you call `useState` many times, you do it in the same order during every render. we'll come back to why this works and when this is useful later.

### But what is a Hook?

Hooks are functions that let you "hook into" React state and lifecycle features from function components. Hooks don't work inside classes - they let you React without classes.

React provides a few builr-in Hooks like `useState`. You can also create your own Hooks to reuse statefil behavior between different components.

## Effect Hook

You'be likely performed data fetching, subscriptions, or manually changing the DOM from React components before. We call these operations "side effects" (or "effects" for short) because they can affect other components and can't be done during rendering.

The Effect Hook, `useEffect`, adds the ability to perform side effects from a function component. It serves the same purpose as `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` in React classes, but unifies into a single API.

For example, this component sets the document title after React updates the DOM:

```javascript
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  // Similar to componentDidMount and componentDidUpdate:
  useEffect(() => {
    // Update the document title using the browser API
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

When you call `useEffect`, you're telling React to run your "effect" function after flushing changes to the DOM. Effects are declared inside the component so they have access to its props and state. By default, React runs the effects after every render - _including_ the first render.

Effects my also optionally specify how to "clean up" after them by returning a function. For example, this component uses an effect to subscribe to a friend's online status, and cleans up by unsubscribing from it:

```javascript
import React, { useState, useEffect } from 'react';

function FriendsStatus(props) {
  const [isOnline, setIsOnline] = useState(null);

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend, id, handleStatusChange);

    return () => {
      ChatAPI.unsubscribeFromFriensStatus(props.friend.id, handleStatusChange);
    };
  });

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```

In this example, React would unsubscribe from our `ChatAPI` when the component unmounts, as well as before re-runnning the effect due to a subsequent render.

Just like with `useState`, you can use more than a single effect in a component:

```javascript
function FriendsStatusWithCounter(props) {
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });

  const [isOnline, setIsOnline] = useState(null);
  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  function handleStatusChange(status) {
    setIsOnline(status, isOnline);
  }
  // ...
}
```

Hooks let you organize side effects in a component by what pieces are related (such as adding and removing a subscription), rather than forcing a split based on lifecycle methods.

## Riles of Hooks

Hooks are Javascript functions, but they impose two additional rules:

- Only call Hooks <b>at the top level</b>. Don't call Hooks inside loops, conditions, or nested functions.
- Only call Hooks <b>from React function components</b>. Don't call Hooks from regular JavaScript functions.

### Reference

- [About Hooks(JP)](https://qiita.com/tatane616/items/01d6358be5e4e4779232)
