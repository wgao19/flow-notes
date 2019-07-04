## Revisiting higher order components

For the scope of this context, I'd like to consider higher order components as *function that takes a component A, and returns a component B which instantiates component A with certain modifications*. 

```js
function makeUnicorn(Creature) {
  return (props) => <Creature {...props} crown="spiraling-horn" />;
}
```

## 2 ways to annotate higher order components

### Explicit annotation

- Wrapped components are aware of and may use injected props
- Export the type of the injected props to be consumed by wrapped components

```js
// makeUnicorn.js
import * as React from 'react';

export type UnicornProps = {|
  decoration: string,
|};

export default function makeUnicorn<P: UnicornProps>
  (Creature: React.AbstractComponent<P>): 
  React.AbstractComponent<$Diff<P, UnicornProps>> {
  return (props) => <Creature {...props} decoration="spiraling-horn" />;
}
```

When using the higher order component, you can import the type of the props injected by this higher order component:

```js
// kittenCorn.js
import * as React from 'react';
import makeUnicorn from './makeUnicorn';
import type { UnicornProps } from './makeUnicorn';

type KittenCornProps = {|
  name: string,
|} & UnicornProps;

const KittenCorn = ({ name, decoration }) => <div>
  {name}
  {decoration}
</div>

export default makeUnicorn(KittenCorn);
```

When we instantiate `KittenCorn`, we no longer need to provide the `decoration` prop.

```js
render(<KittenCorn name="meow" />);
```

### Implicit annotation

- Wrapped components are unaware of injected props or are unaware that the props are injected by a higher order component

[File a PR](https://github.com/wgao19/flow-notes/pulls) to add an example here.

## 2 places to annotate wrapped components

### Explicitly providing type parameters

```js
// kittenCorn.js
import * as React from 'react';
import makeUnicorn from './makeUnicorn';
import type { UnicornProps } from './makeUnicorn';

type KittenCornProps = {|
  name: string,
|} & UnicornProps;

const KittenCorn = ({ name, decoration }: KittenCornProps) => <div>
  {name}
  {decoration}
</div>

export default makeUnicorn<KittenCornProps>(KittenCorn);
```

### Casting at export

```js
// kittenCorn.js
import * as React from 'react';
import makeUnicorn from './makeUnicorn';
import type { UnicornProps } from './makeUnicorn';

type KittenProps = {|
  name: string,
|};

const KittenCorn = (
  { name, decoration }: KittenProps & UnicornProps
) => <div>
  {name}
  {decoration}
</div>

export default (
  makeUnicorn(KittenCorn): React.AbstractComponent<KittenProps>
);
```

## Dealing with nested higher order components

```js
// gloryKittenCorn.js
import * as React from 'react';
import { compose } from 'redux'; // ¯\_(ツ)_/¯
import makeUnicorn from './makeUnicorn';
import type { UnicornProps } from './makeUnicorn';
import glorifyMane from './glorifyMane';
import type { ManeProps } from './glorifyMane';

type KittenProps = { // OwnProps
  name: string
}

const GloryKittenCorn = (
  { name, decoration, mane }: KittenProps & ManeProps & UnicornProps
) => <React.Fragment>
  { name }
  { decoration }
  { mane }
</React.Fragment>;

export default (
  compose(
    makeUnicorn,
    glorifyMane,
  )(KittenCorn): React.AbstractComponent<KittenProps>
)
```

## Take note

- Spreading is tricky in Flow. To avoid complexity, using exact objects for component props is highly recommended.
- Available from v0.89, `React.AbstractComponent` ([link to notes](./react-component-types.md#reactabstractcomponent)) is the most abstract representation of a React component. It allows us to annotate our components with `Props` and optionally an `Instance`. 

## Links

- [HOCs as of 0.89.0](https://flow.org/en/docs/react/hoc/#toc-hocs-as-of-0-89-0) from Flow's official doc
- [`React.AbstractComponent`](https://flow.org/en/docs/react/types/#toc-react-abstractcomponent)
- [React Higher Order Components in Depth](https://medium.com/@franleplant/react-higher-order-components-in-depth-cf9032ee6c3e)
