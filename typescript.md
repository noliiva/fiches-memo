# Typescript memo
## React useful types
Extract props types from a component
```
React.ComponentProps<typeof MyComponent>["myProp"]
```

\
Component style prop type
```
React.CSSProperties
```

\
Enum of all HTML elements accepted as React Components (e.g. h1, p, span, ...)\
Cf. [React Typescript cheatsheet](https://react-typescript-cheatsheet.netlify.app/docs/advanced/patterns_by_usecase/#polymorphic-components-eg-with-as-props)
```
React.ElementType<any>
```

\
Type a timeout ref
```
const timeoutRef = useRef<NodeJS.Timeout>();
```

\
Extract enum from array
```
const myArray = ['v1', 'v2', ...] as const;
type ArrayValues = (typeof myArray)[number]; // 'v1' | 'v2' | ...
```
