# Typescript memo
## React useful types

Extract props types from a component
``` ts
React.ComponentProps<typeof MyComponent>["myProp"]
```

\
Component style prop type
``` ts
React.CSSProperties
```

\
Enum of all HTML elements accepted as React Components (e.g. h1, p, span, ...)\
Cf. [React Typescript cheatsheet](https://react-typescript-cheatsheet.netlify.app/docs/advanced/patterns_by_usecase/#polymorphic-components-eg-with-as-props)
``` ts
React.ElementType<any>
```

\
Type a timeout ref
``` ts
const timeoutRef = useRef<NodeJS.Timeout>();
```

\
Extract enum from array
``` ts
const myArray = ['v1', 'v2', ...] as const;
type ArrayValues = (typeof myArray)[number]; // 'v1' | 'v2' | ...
```

## Tuples

Named Tuples. Useful for naming function args.
``` ts
const T = [myName: string];

function myFunc(...args: [string]) {}
//  ⤤ function myFunc = (args_0: string) => void

function myFunc(...args: [myParam: string]) {}
//  ⤤ function myFunc = (myParam: string) => void
```

## Generics
``` ts
function myFunc<T>(t: T) { ... };
const myFunc = <T>(t: T) => { ... };
class Component<T> { ... }
```

\
Generics allow finer type inference.

``` ts
const returnWhatIPassIn = <T>(param: T) => param;
returnWhatIPassIn(1) // const returnWhatIPassIn: <1>(t: 1) => 1
```

\
Generic can be constrained with `extends`;

``` ts
const myFunc = <T extends string>(t: T) => t;

const inferItemLiteral = <T extends string | number>(t: T) => t;
```

\
Generic can have a default type;

``` ts
const createSet = <T = string>() => new Set<T>();
```

\
Type arguments can constrain the type of a func's args.
``` ts
const returnWhatIPassIn = <T>(param: T) => param;
returnWhatIPassIn<number>('my string'); // Argument of type 'string' is not assignable to parameter of type 'number'.
```

\
Properly typing a reduce prevent initial value error.
``` ts
const obj = array.reduce<Record<string, { name: string }>>((accum, item) => {
  accum[item.name] = item;
  return accum;
}, {});
```

\
Fix `any` as soon as possible. Usefull for libs func that don't have Type Argument.
``` ts
const fetchData = async <TData>(url: string) => {
  let data: TData = await fetch(url).then((response) => response.json());
  return data;
};
```

\
Enforce Generic definition by using a default type to display an error message. (Won't work with constrained types)
``` ts
const fetchData = async <TResult = "You must pass a type argument to fetchData">(url: string): Promise<TResult> => {
  const data = await fetch(url).then((response) => response.json());
  return data;
};
const data = await fetchData("https://swapi.dev/api/people/1");
//  ⤤ const data: unknown;

const fetchData = async <TResult = "You must pass a type argument to fetchData">(url: string): Promise<TResult> => {
  const data = await fetch(url).then((response) => response.json());
  return data;
};
//  ⤤ const data: "You must pass a type argument to fetchData"
```

\[
Typing dynamic function args](https://github.com/total-typescript/typescript-generics-workshop/blob/main/src/06-challenges/29.2-dynamic-function-arguments.solution.ts)

\
Always represent generics with a low-level type. ([source 1](https://github.com/total-typescript/typescript-generics-workshop/blob/main/src/03-art-of-type-arguments/12-generics-at-different-levels.solution.1.ts), [source 2](https://github.com/total-typescript/typescript-generics-workshop/blob/main/src/03-art-of-type-arguments/12-generics-at-different-levels.solution.1.ts))
``` ts
const getHomePageFeatureFlags = <
  TConfig extends {
    rawConfig: {
      featureFlags: {
        homePage: any;
      };
    };
  }
>(
  config: TConfig,
  override: (
    flags: TConfig["rawConfig"]["featureFlags"]["homePage"]
  ) => TConfig["rawConfig"]["featureFlags"]["homePage"]
) => {
  return override(config.rawConfig.featureFlags.homePage);
};

//  ⤤ Capture the whole config object in the Type Argument
//  const getHomePageFeatureFlags: <{
//    apiEndpoint: string;
//    apiVersion: string;
//    apiKey: string;
//    rawConfig: {
//        featureFlags: {
//            homePage: {
//                showBanner: boolean;
//                showLogOut: boolean;
//            };
//            loginPage: {
//                showCaptcha: boolean;
//                showConfirmPassword: boolean;
//            };
//        };
//    };
//  }>( ... ) => { ... }

const getHomePageFeatureFlags = <HomePageFlags>(
  config: {
    rawConfig: {
      featureFlags: {
        homePage: HomePageFlags;
      };
    };
  },
  override: (flags: HomePageFlags) => HomePageFlags
) => {
  return override(config.rawConfig.featureFlags.homePage);
};

//  ⤤ Capture only what's really useful to the func in the Type Argument
// const getHomePageFeatureFlags: <{
//   showBanner: boolean;
//   showLogOut: boolean;
//  }>( ... ) => { ... }

// ===== //

const typedObjectKeys = <TKey extends string>(obj: Record<TKey, any>) => {
  return Object.keys(obj) as Array<TKey>;
};

// ===== //

const getStatuses = <TStatuses extends string[]>(statuses: TStatuses) => {}
// ⤤ ReturnType = Array<string>

const getStatuses = <TStatus extends string>(statuses: TStatus[]) => {
  return statuses;
}
// ⤤ ReturnType: Array<"INFO" | "DEBUG" | "ERROR" | "WARNING">
// This allow to infer members of the array
```

\
Factory Function allow to chain type inference. ([see 1](https://github.com/total-typescript/typescript-generics-workshop/blob/main/src/03-art-of-type-arguments/14-safe-function.solution.2.ts), [see 2](https://github.com/total-typescript/typescript-generics-workshop/blob/main/src/04-generics-advanced/20.6-reusable-context.solution.ts), [see 3](https://github.com/total-typescript/typescript-generics-workshop/blob/main/src/04-generics-advanced/20.7-working-around-partial-inference.solution.ts))

\
Where you put the type argument matters to how it's going to be inferred.
``` ts
const acceptsValueInAnObject = <T>(obj: { input: T }) => {
  return obj.input
}
// ⤤ ReturnType infered as string

const result = acceptsValueInAnObject({ input: "abc" } as const)
// ⤤ ReturnType is "abc" as obj is cast to a litteral with const.

const acceptsValueWithObjectConstraint = <T extends { input: string }>(obj: T) => {
  return obj.input
}
// ⤤ ReturnType = string as the constraint is on a global object.

const acceptsValueInAnObjectFieldWithConstraint = <T extends string>(obj: { input: T}) => {
  return obj.input
}
// ⤤ ReturnType = "abc".
```

\
TS limitations
``` ts
function youSayGoodbyeISayHello<TGreeting extends "hello" | "goodbye">(
  greeting: TGreeting,
): TGreeting extends "hello" ? "goodbye" : "hello" {
  return (greeting === "goodbye" ? "hello" : "goodbye") as any;
}
// ⤤ as any is needed here as TS is not powerful enough to interpret the ternary.

function remapPerson<Key extends keyof Person>(
  key: Key,
  value: Person[Key],
): Person[Key] {
  if (key === "birthdate") {
    return new Date() as Person[Key];
  }
  return value;
}
```

``` ts
const getValue = <TObj, TKey extends keyof TObj>(obj: TObj, key: TKey) => {
  return obj[key];
};

const obj = {
  a: 1,
  b: "some-string",
  c: true,
};

const numberResult = getValue(obj, "a");  // number
const stringResult = getValue(obj, "b"); // string
const booleanResult = getValue(obj, "c"); // boolean
```

## Function overloads

Useful when a func can accept a different set of parameters and func return a value type depending on what is passed in.
If func return the same type no matter which set of parameters, a Union is preferrable.
Function overloards work only for function not for function declared with const.
``` ts
function youSayGoodbyeISayHello(greeting: "goodbye"): "hello";
function youSayGoodbyeISayHello(greeting: "hello"): "goodbye";
function youSayGoodbyeISayHello(greeting: "goodbye" | "hello") {
  return greeting === "goodbye" ? "hello" : "goodbye";
}
```
