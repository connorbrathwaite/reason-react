---
title: Context & Mixins
---

## Context

In order to use React's context, you need to create two things:
1. The context itself
2. A context provider component.

```reason
/** ContextProvider.re */
let themeContext = React.createContext("light");

let makeProps = (~value, ~children, ()) => {
  "value": value,
  "children": children,
};

let make = React.Context.provider(themeContext);
```

That will give you a `ContextProvider` component you can use in your application later on. You'll do this like you'd normally would in any React application.

```reason
/** App.re */
[@react.component]
let make = () =>
  <div>
    <ContextProvider value="light">
      <ComponentToConsumeTheContext />
    </ContextProvider>
  </div>
```

Also, you can consume the context by using the `React.useContext` hook

```reason
/** ComponentToConsumeTheContext.re */
[@react.component]
let make = () => {
  let theme = React.useContext(ContextProvider.themeContext);

  <h1>theme->React.string</h1>
}
```

## Mixins 
ReasonReact doesn't support ReactJS mixins. Composing normal functions is a good alternative.
