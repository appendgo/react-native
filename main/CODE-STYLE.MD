# React-Native Development Guidelines

## Specific and Descriptive File Names

### Bad Examples
* `NewScreen`

### Good Examples
* `DocumentNewScreen`

## Method Order in Class Components

Aim: Arrange methods in a top-down order.

1. `context`
2. `__constructor`
3. Lifecycle methods
4. `render`
5. `renderXY`
6. Other methods

## Default Exports

- Use default export inline with the class declaration, except when using Redux's `connect`.
