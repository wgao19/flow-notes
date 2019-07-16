## Exact v.s. Sealed

Exact means the object passed in here _must not_ contain extra fields ([link to doc](https://flow.org/en/docs/types/objects/#toc-exact-object-types)).

Sealed, on the other hand, means the object may contain other fields but you may not access them unless you annotate them. When we write an object type with some fields, it is by default _sealed_. Trying to access unannotated field of a sealed object will result in error, regardless of it being exact or not:

```js
type Sealed = { foo: string }

const sealed = {
  foo: 'foo',
}
sealed.bar = 'bar' // error
const { foo, bar } = sealed // error
```

Currently, objects are by default sealed and inexact. However, Flow is on [the roadmap of migrating to by default exact](https://medium.com/flow-type/on-the-roadmap-exact-objects-by-default-16b72933c5cf).

For functions that expect sealed objects, you can still pass in objects with extra props.

```js
function usingSealed(x: Sealed) {
  // does things
}
usingSealed({ foo: 'foo', bar: 'bar' }) // ok
```

Not so when the functions are expecting _exact_ objects:

```js
type Exact = {| foo: string |}

function usingExact(x: Exact) {
  // does things
}
usingExact({ foo: 'foo', bar: 'bar' }) // error
```

We may access the fields of function parameters by destructuring the object:

```js
// destructuring on function parameter
function goodUsingSealed({ foo }: Sealed) { // ok
  // does things
}
```

But since destructuring means accessing the object, we _should not_ be able to access extra props to sealed objects. This is fixed in 0.100:

```js
// fixed in 0.100
function badUsingSealed({ foo, bar }: Sealed) { // error after 0.100
  // does things
}
```

- [Try Flow](https://flow.org/try/#0C4TwDgpgBAyhCGAbCATKBeKBvKAzA9vgFxQDOwATgJYB2A5lAL4DcAUKJFAKIAe8AxsAzYAPnkIly1elBEtWrfvhrkyCZGkxZWUccSgByAvgOtGrUutQA6AEbwKwg-YoHmUAPQeoEChXwUisqqOMYANFAuTMKWSKjuXj5+AQq4AK40glTKUGmktHRwcSgAFDwkRRoAlNg6nt4o+BCkUMAAFgWkZqx5BZWoJaEShsYGES4kzg4GTFUJ3vgA1qkZWTm99LwCwGUkW4I12rqJjc2tHfRd5ht0+ztD+kaEY5EOky4zjHMAkIm+-oFWCdmpQ0oI0tIGDl0plgNkaFAwA54ABbCDAXysGFrBF0QgoACq+Xo-VKDyYFSsKEO9SgSzqJyaLXanTMbCB3lwVB4qCgtCgAAZrABGAUCrGrOE5eyE4mFKmDPTjBwU2BUml-ZKOeC4DGOIWi8XHBpM86s8xAA)


References
---
- [On the Roadmap: Exact Objects by Default](https://medium.com/flow-type/on-the-roadmap-exact-objects-by-default-16b72933c5cf)
