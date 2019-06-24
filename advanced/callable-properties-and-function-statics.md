## Callable Properties and Function Statics

You can annotate functions as callable objects, i.e.,

```js
type F = {
  (): string,
};

const f: F = () => 'hello';
```

A function or a callable object may have multiple callable properties, also known as overloading.

Note that a few syntax are supported when annotating callable properties:

```js
type F = {
  (): string,   
  (x: boolean): string,
  [[call]](x: number): string,   
  [[call]]: string => string,
};

// It will be fine when a function satisfies them all
const f: F = (x?: boolean | number | string) => {
  return x ? x.toString() : '';
}

// And Flow will notice when the function doesn't satisfy them all
const g: F = (x?: number | string) => { // $ExpectError
  return x ? x.toString() : '';
}
```

Callable objects can be viewed equivalently as functions with static fields. Function type statics are initially `{}`. Flow will notice when you annotate a variable as function type and try to access its statics without annotation.

```js
type F = () => void;

const f: F = () => {
  f.foo = 'bar'; // $ExpectError "missing in statics of function type"
}
```

You can annotate function with statics as objects with callable fields. This can be useful when annotating a memoized function:

```js
type MemoizedFactorial = {
  cache: {
    [number]: number,
  },
  [[call]](number): number,
}

const factorial: MemoizedFactorial = n => {
  if (!factorial.cache) {
    factorial.cache = {}
  }
  if (factorial.cache[n] !== undefined) {
    return factorial.cache[n]
  }
  factorial.cache[n] = n === 0 ? 1 : n * factorial(n - 1)
  return factorial.cache[n]
}
```

References
---

- [Function statics and callable properties on TypeScript v.s. Flow](https://github.com/niieani/typescript-vs-flowtype/pull/55)

Recent changes

- [Fix implicit proto for objects with `[[call]]` properties](https://github.com/facebook/flow/commit/5d7e01d06b85388882b3214e383d26b73e6de111)
- [Model multiple call properties as an intersection of callable objects](https://github.com/facebook/flow/commit/b9e26fd3bf7ba10e8f2f8c4e9c90d7f92afe96e1)
- [Concretize callable object params before intersection processing](https://github.com/facebook/flow/commit/0938da8d7293d0077fbe95c3a3e0eebadb57b012)
- [Remove `[[call]]` property from function statics](https://github.com/facebook/flow/commit/3c5a41026f8da473b3869e0ef6d84afa0b978816)

A while ago when it was born

- [Store object call properties in internal slot](https://github.com/facebook/flow/commit/b9db648afe4f2207a49985aa82b90a485a11a900)
- [Add support for `[[call]]` internal slot properties](https://github.com/facebook/flow/commit/954a72704a6338778c940239573045b28c716488)
