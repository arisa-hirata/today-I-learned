# What are Redux selectors? Why use them?

Selectors are functions that take Redux state as an argument and return some data to pass the component. <br/>
They can be as simple as:

```javascript
const getDataType = state => state.editor.dataType;
```

Or they can do more complicated data transformations like filter a list.
They are typically used in `mapStateToProps` in `react-redux`'s `connect`:<br/>
For example this

```javascript
export default connect(state => ({
  dataType: state.editor.dataType
}))(MyComponent);
```

becomes this:

```javascript
export default connect(state => ({
  dataType: getDataType(state)
}))(MyComponent);
```

### Why?

One reason is to avoid duplication data in Redux.

Redux state can be thought of like a database and selectors like SELECT queries to get useful data from the database. A good example is a filtered list.

If we have a list of items in Redux but want to show a filtered list of the items in the UI, we could filter the list, store it in Redux then pass it to the component. The problem is there are two copies of some of the items and it is easier for data to get out of sync. If we wanted to update an item, we'd have to update it in two places.

With selectors, a `filterBy` value would be stored in Redux and a selector would be used to compute the filtered list from
the Redux state.

### Why not perform the data transformations in the component?

Performing data transformations in the component makes them more coupled to the Redux state and less generic/reusable. Also, as Dan Abramov points out, it makes sense to keep selectors near reducers because they operate on the same state. If the state schema changes, it is easier to update the selectors than to update the components.

### Performance

`mapStateToProps` gets called a lot so performing expensive calcurations there is not good. This is where the `reselect` library comes in. Selectors created with `reselect`' `createSelector` will memorize to avoid unneccessary recalculations.

✔︎If perdormance is not an issue, `createSelector` is not needed.

### References

- [Dan Abramov's video](https://egghead.io/lessons/javascript-redux-colocating-selectors-with-reducers)
- [Redux docs on selectors](https://redux.js.org/recipes/computing-derived-data)
- [Reselect](https://github.com/reactjs/reselect)
