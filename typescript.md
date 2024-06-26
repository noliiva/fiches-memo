# Typescript memo

Extract props types from a component
```
React.ComponentProps<typeof MyComponent>["myProp"]
```

React acceptable string as Component (e.g. h1, p, span, ...)
```
React.ElementType<any, keyof React.JSX.IntrinsicElements>
```
