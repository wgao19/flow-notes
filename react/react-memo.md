## `React.memo`

`React.memo`, with `memo` for _memoization_, is used on functional components that are supposed to render the same result given the same props.

The signature of `React.memo` is as follows:

```js
declare export function memo<Config, Instance = mixed>(
  component: React$AbstractComponent<Config, Instance>,
  equal?: (Config, Config) => boolean
): React$AbstractComponent<Config, Instance>
```

And we can use it this way:

```jsx
// @flow
const React = require('react')

type Props = {| cornStyle: 'spiraling' | 'colorful' |}
function Unicorn(x: Props) {
  return null
}
const MemoUnicorn = React.memo<Props>(Unicorn)

const memo_unicorn_ok = <MemoUnicorn cornStyle="spiraling" /> // ok
const memo_unicorn_error = <MemoUnicorn corn="spiraling" /> // error
```

We may optionally provide an `equal` method as a [performance optimization](https://reactjs.org/docs/optimizing-performance.html). `memo` provides the type information for the method with the same props type we supplied, and we don't need any extra type annotations for it. And since we did provide a `Props` type parameter to `React.memo`, Flow is able to catch errors on the `equal` method:

<!-- prettier-ignore-start -->
```jsx
const memo_unicorn_with_equal_ok = 
      React.memo<Props>(Unicorn, (props1, props2) => props1.cornStyle === props2.cornStyle); // ok

const memo_unicorn_with_equal_error = 
      React.memo<Props>(Unicorn, (props1, props2) => props1.corn === props2.corn); // error
```
<!-- prettier-ignore-end -->

And we can pass the returns of `React.forwardRef` to `memo`:

```jsx
const { useImperativeHandle } = React

function Demo(props, ref) {
  useImperativeHandle(ref, () => ({
    moo(x: string) {},
  }))
  return null
}

const Memo = React.memo(React.forwardRef(Demo))

function App() {
  // Error below: moo expects a string, given a number
  return <Memo ref={ref => ref && ref.moo(0)} />
}
```
- [Flow Try: `React.memo`](https://flow.org/try/#0PTACDMBsHsHcCgDG0B2BnALgAgEoFMBDRbAXiwCc8BHAVwEtKAKAckqI2YEp54MBPAA54sABXLQBaLGQDeAHyzJyKAMr9IeAFxZmaAQwKQ6KAObMsC5shjlwNSObkBfHnZTE6qLAFUUdJSiMAB7aYhJonFgy8FgUeBg0ylgo9pDwLkiomFgAsngAttC+-tBJZPjsAHT5BdAAPGGSAHyMxQHcmejYNYUA+jR+Ab3QANbSWHV5hW2lKIqzanwaJABEegZGpitYwE0A3DvAWKOd2T3Q-YOzvXjk4uTjk7UzSQGr6+SGxibbuwexICwt3uPEBAHVhIgCHMBOIAG50AAmwmhQNohiwNQwAAtoIisBhoFgAAYVYjVWrEzSnbq1S4lZS9WB0HE3dGQYZjMgxWK8skYCmFBriZqtK7KAA0WEYsPCAEYpbLJAAmSIkJpYJVoOWVAKLDTSEhkLXK3ULdR4TgHQEneCAgBiMFgWDoUgIACMDYTFAQMIhsUC7qUpF58q78r7-Xh8UqCYI8CG5jjhNQaBisbjETTMXSBgyUEyWdi2WmOcDSuMebzcIRyedheEWi8UFKZSLtYr26rpBqtTqAobjV2zcorYdAyDQUcIT6YQQ0FJk3EEsoQ+ASfzKuBSrACOREfhwMSCUTiecqTxkF0olgaGg8ABJfJCT4YOhwvAACWhiINTnG-KuAMHheAAIrUbbhFKlDgJE0SxHej7Prcvrvl+P4aIwMGtmqGqMPBvKFNAwTaJg5DfHBTgSjyTicNwsSUCucwpJAaQZFe2RTES5S1gK5yMJu27kLu+6How4GFHRQHuG+XgAIICAIjBwTygIAKJBg87p4E62hEUCQRCMQbpYGR3xSiYaFzAQyQ0Pk2nkDyjGJHMTyFHE4AkDIME9h5WAAGT+R51TQMRAAMnD-rs6RAA)

References
---
- [Update React.memo and React.lazy to account for refs](https://github.com/facebook/flow/commit/76b78fa56b06e2e958c5a981271632663c26cd42) in [v0.101](https://github.com/facebook/flow/releases/tag/v0.101.0)
- [React.memo](https://reactjs.org/docs/react-api.html#reactmemo)
