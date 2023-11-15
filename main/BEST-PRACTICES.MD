# React-Native Development Best Practices

## Descriptive Action Naming
When you have multiple actions like `fetchClientsAction` in the project that fetch clients in different ways, include the screen or module name in each `fetchClientsAction` for clarity.

## Class-Level Arrow Functions as Props

### Avoid:
* Inline functions
* Bound functions

### Reason:
- Using bind or inline functions in render causes them to be treated as new instances, leading to re-rendering of the component. 
- Class-level arrow functions re-render only if they contain a state or prop that has changed.
- If binding to something other than the current `this`, do it in the constructor.

### Bad Example:
```javascript
export default class SingleSelectList extends Component {
  render() {
    return (
      <FlatList
        renderItem={this.renderItem.bind(this)}      // bound func
        onScrollToIndexFailed={() => {}}             // inline func
        initialScrollIndex={this.props.selectedIndex}
      />
    );
  }

  renderItem() {
  }
}
```

### Good Example:
```javascript
export default class SingleSelectList extends Component {
  render() {
    return (
      <FlatList
        renderItem={this.renderItem}                        // class-level arrow function
        onScrollToIndexFailed={this.onScrollToIndexFailed}  // class-level arrow function
        initialScrollIndex={this.props.selectedIndex}
      />
    );
  }

  renderItem = () => {
  }

  onScrollToIndexFailed = () => {
  }
}
```

## mapStateToProps Usage

* Create only a single level return object in `mapStoreToProps`.
* Use the `store` prefix to differentiate between Component state and Redux Store state.

### Bad Example:
```javascript
const mapStoreToProps = store => ({
  store: {
    transactions: {
      ...store.transaction.transactions,
      isEmpty: store.transaction.transactions.data === null ||
               store.transaction.transactions.data.length === 0,
    },
  },
});
```

### Good Example:
```javascript
const mapStoreToProps = store => ({
  storeTransactions: store.transaction.transactions,
  storeIsEmptyTransactions: store.transaction.transactions.data === null ||
                            store.transaction.transactions.data.length === 0,
});
```

## Using Reselect Library

* Use for calculated values like `map`, `filter`.
* Prevents recalculations on every render, only recalculates when the input parameters change.

```javascript
const selectFilteredClientData = createSelector(
  // ... [selectors and calculation logic]
);

const mapStoreToProps = store => ({
  // ... [mapped properties]
});
```

## Component State and Redux State Reset

* Perform resets in `componentWillUnmount`.
* Ensures that the render before `componentDidMount` happens with an empty state.
* Useful for rendering placeholders.

## State Usage

* Only use state if it impacts rendering.
* State changes trigger re-renders.
