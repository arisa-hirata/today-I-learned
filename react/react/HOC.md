# React Higer Order Components

### What are they?

A pattern for when we find ourselves repeating logic across components. They are not part of the `React` API.

### What do they do?

They are functions that take components and return new components.

### When to use?

When you are repeating patterns/logic across components.

#### Examples;

- hooking into/subscribing to a data source
- adding interactivity to UI (<i>also achived with wrapper/render props</i>)
- sorting/filtering input data

### An Example

We have a `Mouse` component.

```javascript
const Mouse = () => (
  <span className="mouse" role="img">
    🐭
  </span>
);
```

And make it `Deaggable` using
