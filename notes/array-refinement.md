## Array Refinement

If you have an Array of [Maybe](https://flow.org/en/docs/types/maybe/) objects, and you want to filter out `null`, you can 

```js
function getArray(): Array<?{}> {
  return [{}, {}, null, null, {}];
}

const array: Array<{}> = getArray().filter(Boolean);
```

References
---

- [Refine array types using `filter`](https://github.com/facebook/flow/issues/1414)
- [Refinement Invalidations](https://flow.org/en/docs/lang/refinements/#toc-refinement-invalidations)