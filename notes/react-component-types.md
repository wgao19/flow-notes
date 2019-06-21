🚧 Copied from [Notes on 0.100](https://dev.wgao19.cc/2019-06-13__flow-0.100/), needs refinement and revision.

## React component types


There are a bunch of changes around React library definitions. And so it's a good chance to take a step back and look at what they are in all.

[Here](https://github.com/facebook/flow/blob/master/lib/react.js) is the link to the React library definitions by Flow.

My list of commonly used:

- `React$Component<Props, State = void>`
- `AbstractComponent<-Config, +Instance = mixed>`
- `React$ComponentType<-Config>`
- `React$ElementType`
- `React$Element<+ElementType: React$ElementType>`
- (new) `React$MixedElement = React$Element<React$ElementType>`
- (new) `MixedElement = React$MixedElement`
- `React$Ref<ElementType: React$ElementType>`

In the definitions above, those with the angled brackets are polymorphic types. This means you'll need to supply type parameters for those polymorphics.

### `React$Component<Props, State = void>`

`React$Component` is the base class of ES6 React classes, modeled as a polymorphic class whose main type parameters are Props and State.

### `React$AbstractComponent`

`React$AbstractComponent` is the type name used by Flow, and is used by a few different types of React classes and components in React's library declarations.

`React.AbstractComponent` uses it directly, which takes two parameters, `Config` for the props type, and `Instance` for an instance. Functional components have `Instance: void`.

### `React$ComponentType`

```jsx
declare type React$ComponentType<-Config> = React$AbstractComponent<
  Config,
  mixed
>
```

Aliased to `React$AbstractComponent<Config, mixed>`, and is used as the type of a component in React. It can be:

- Stateless functional components. Functions that take in props as an argument and return a React node.
- ES6 class component. Components with state defined either using the ES6 class syntax, or with the legacy `React.createClass()` helper.

### `React$ElementType`

```jsx
declare type React$ElementType = string | React$AbstractComponent<empty, mixed>
```

The type of an element in React. A React element may be a:

- `string`: These elements are intrinsics that depend on the React renderer implementation.
- React component. See `ComponentType` for more information about its different variants.

A few more related with `ElementType`:

A `React$Element` is the type of a React element. React elements are commonly created using JSX literals, which desugar to React.createElement calls (see below).

```jsx
declare type React$Element<+ElementType: React$ElementType> = {|
  +type: ElementType,
  +props: React$ElementProps<ElementType>,
  +key: React$Key | null,
  +ref: any,
|}
```

Finally, here are the two new types:

```jsx
declare type React$MixedElement = React$Element<React$ElementType>
declare type MixedElement = React$MixedElement
```

A keen reader may have noticed that above is more or less a copy and paste of comments and code snippets from Flow's codebase. They are really very well-written and a significant portion of the code itself is self-explanatory.
