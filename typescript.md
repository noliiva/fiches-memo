# Typescript memo

Extract props types from a component
```
React.ComponentProps<typeof MyComponent>["myProp"]
```
\
React acceptable string as Component (e.g. h1, p, span, ...)\
Cf. [React Typescript cheatsheet](https://react-typescript-cheatsheet.netlify.app/docs/advanced/patterns_by_usecase/#polymorphic-components-eg-with-as-props)
```
React.ElementType<any>
```
