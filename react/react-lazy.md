## `React.lazy`

`React.lazy` currently lets us render a dynamic import as a regular component. The signature of `React.lazy` tells us that it takes an async function which resolves to a module export, which in turn contains a `default` field:

```jsx
declare export function lazy<P>(
  component: () => Promise<{ default: React$ComponentType<P>, ... }>
): React$ComponentType<P>
```

Here's how we may annotate a `React.lazy` loaded funcitonal component:

```jsx
//@flow
const React = require('react')

type Props = {| cornStyle: 'spiraling' | 'colorful' |}

function Unicorn(x: Props) {
  return null
}

const LazyFunctionComponent = React.lazy(() =>
  Promise.resolve({ default: Unicorn })
)

const lazy_unicorn_ok = () => <LazyUnicorn cornStyle="spiraling" /> // ok
const lazy_unicorn_error = () => <LazyUnicorn corn="spiraling" /> // error
```

We can pass the returns of `React.forwardRef` to `React.lazy`:

```jsx
const { useImperativeHandle } = React

function Demo(props, ref) {
  useImperativeHandle(ref, () => ({
    moo(x: string) {},
  }))
  return null
}

const Lazy = React.lazy(async () => ({
  default: React.forwardRef(Demo),
}))

function App() {
  // Error below: moo expects a string, given a number
  return (
    <React.Suspense fallback="Loading...">
      <Lazy ref={ref => ref && ref.moo(0)} />;
    </React.Suspense>
  )
}
```

- [Flow Try: `React.lazy`](https://flow.org/try/#0PTACDMBsHsHcCgDG0B2BnALgAgEoFMBDRbAXiwCc8BHAVwEtKAKAckqI2YEp54MBPAA54sABXLQBaLGQDeAHyzJyKAMr9IeAFxZmaAQwKQ6KAObMsC5shjlwNSObkBfHnZTE6qLAFUUdJSiMAB7aYhJonFgy8FgUeBg0ylgo9pDwLkiomFgAMgQAXny+-tBJZPjsAHSQBXwAPGGSAHyMMViMkSRNouIAtnRoeJWUaNCQAG54jDIAJnjgBPYY2sUBTtycANw8yOjYNYUA+jR+AYfQANbS7Z3ddXmFq6Uois9qfBokAER6BkamXywwG6ICwl0yeywBz4x1Oz0OeHI4nI1w60juDyKcKSAW+v3IhmMJkBwKBwCwiORPFBAHVhIgCC8BAQ0FIMAALYSUBLKKTQcBYAAGFWIlXApVgBHIM3w4EFWAw0CF0MFmh2WWwMiwNEGAElekICRg6JMABKMmYaLBOa4ijCuE4eLwAETwvWgjAE4kkABo4uBItFYjq8PrDQRjWaLRpGJRwH60V12kHYlh3R6QlhMOQiYGnD62utuLFuYkXilIGkMrtspjbYRRdDGCy+O4bujk205gslto7WKJVKZfNGK73ZwC0WHe5jV4AIICARolOggCiSNKWAARngYLBtOmKUEhMQpAQsxgc6Y-SYTXgXueUr0d+Q2qWkq1U1g6v2VDqhOgwgLJWW5EBc3w5NABAzESlRwV8TRtF+9y1P6JAyHGHaYQAZNh-qVOmjAAAycDawLbMhwC-v+96DIhsTcE4QA)

References
---
- [Update React.memo and React.lazy to account for refs](https://github.com/facebook/flow/commit/76b78fa56b06e2e958c5a981271632663c26cd42), updated in [v0.101](https://github.com/facebook/flow/releases/tag/v0.101.0)
- [`React.lazy` docs](https://reactjs.org/docs/code-splitting.html#reactlazy)
