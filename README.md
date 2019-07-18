# Flow Notes

📝 Notes on using and understanding Flow, starting from version 0.85.

🚧 This repo is a work in progress.

- [Umbrella issue](https://github.com/wgao19/flow-notes/issues/1)

## Basics

https://flow.org/en/docs/lang/

### Objects 

[https://flow.org/en/docs/types/objects/](https://flow.org/en/docs/types/objects/)

Familiar yourself with objects by reading the docs. It covers such questions as

- [Basic syntax for typing objects](https://flow.org/en/docs/types/objects/#toc-object-type-syntax)
- [Optional and nullable properties](https://flow.org/en/docs/types/objects/#toc-optional-object-type-properties)
- [What are sealed objects?](https://flow.org/en/docs/types/objects/#toc-sealed-objects)
- [What are unsealed objects?](https://flow.org/en/docs/types/objects/#toc-unsealed-objects)
- [What are exact objects?](https://flow.org/en/docs/types/objects/#toc-exact-object-types)
- [How to use indexer properties?](https://flow.org/en/docs/types/objects/#toc-objects-as-maps)
- [What are the differences among `{}`, `Object`, and `{ [key: string]: any }` ?](https://flow.org/en/docs/types/objects/#toc-object-type)

**Examples** ([Flow Try](https://flow.org/try/#0C4TwDgpgBAcghgW2gXgFBSgHygIgMoCWCARnDulrgLICuAZnAM5kXY7wA2LGbecATnGIFyPXH0F0CAO26V8AYwGj5AaQIC5bVQHsAbjRVsAagWBxpIgNypUCndMbAoAcQCiMACJuASlGRQAN4UVACCADJuAFy4CHAcEDgANBQAYm5hkTE4dBBxCeQAvjZ2Dk5QYDT8-Iz+QRTE-AQQdNlg1ckU0jr8+W3V-J0YHA4A5v0DgykYMszSEBOTS8srq2urRSWgkFDqwMAQ0nWB2AD0p1D8EPYISNIAJlA0jDKjUIwQ8RCPFo8QAB5wBTOHTEABW12AjFsGFOACo4VBSC8FFApBAOPdanDThQuogIABGGJOJrSUbTKCyJAAJhi5yg9wIjDBOhkzholgcaJ6UAQPWgVyk80e21eFDE+CIpBUktoDGYsvknDkkokQhEEvk6uFqu1SkGWu0GkESu0+kMRtwpnMliGVIJAGYYvAkEkoAzttB4hpanReZ8XhB+JcIM9vQ9Q3B7hqOGYQHiMHBRgsqTQSMHKRQUw9gzEACTGeI0CCMAA8Xp0dFcHm8PgAfO6GQByfIQZuUZu5NvNxMVKo1AuqCAgcuV6uVaqMRsei7NxrNOgd7DN7q9eLLqDNkbkzfN2YWdswj0ItGc4EEbnozHY3EYCiT-jEqCpc-AS-SJsXbrOK43O73N8SLXHA4Yvm+H5QMyVI6AA7lAPpMEBwA6FAAAGFggGhD4DnSUAABQAJT+PWQSFF+UBxgA1hiIAIVA2w6O6TKPCAOg0HynxHERJFQHobL3AA-Mej7OgRxHIKR-EEPcFH4XowZ0f+DjEXAZ7SBe3LAAAFnAzj3DopbSM2zjmDRMEhlcwBVEcmE6eKGCPgALCSwBkm8kl8QJckKfwSk6LcKk4dUACsMT4dSqakq8EmkcQOg6AkFg+YpUDKdIxFgZFjxgJoSAHCG-ohsQED7MGUYxsIcagMe8KIqCELAmizQ3lAOIUHE8zPgA8uCkIUT+ob-ocgH3B1h54YE5GzjBv7XAFAHfDEg0QApRwfF8slUp8-AcHROnQMwSAIbUmHjfMjqCTEgQzToYDvg48TNRiW1IBYrwMdp0HXo8cR0byf2zVAALMsAWoANo0SArnuQAujEmEzUoRwlfRXDlFcjA9M4BDVmxHFXPEe2Mg4JlQFR3TwbBunAM2tSjGy5JQA4FDkX2nUQC5UCCTdDLSDQHBcMQCTum9lhM-ZfotY8yPAWmgvMyGnKAcK3xavYIz8DDrwpX5aULSpUCwWY2mMi0MhAe0d3Bu+pZal62Qczg8glQI9zO2wCDPOYCjaYkrNZhgHOMFd3P4bzFw-bUsuo-FOnM-dH5Pb88tCwk6uJT02vkpSGAO7Eh4e7grv8O78he04QJ+yohTg7DxEMgIgj-dWDWQtCmDFLY9iOM4VFmAc0gxHsg-HPiSDPs2-dlcZlKRXhzaECQcDNnPToxM2KqrxQyapgA7JSOaAVrW49gNOgHJ9emfdBXpQbUxuASKwWDluC4tKvM0V84qMONAVafWgNVYM8RoSOQHM+Hinkbo9yxgkAAdCMUY+FmztH4M2YibNwHVDwlA0i4dCiEUpKJcKsUgj60cIlCAiCdDINQdUDBUAsH9mqFzSKvEYFlCoTQ5B7CADUW53RoIGIw5hj4woOmOp5AAhNIyKlIObPimgoia11mEczEpwzWG8Yz8Coo0OCxkmEqPmFzLRWcty6P0fwQxn987zh2vcDs6jDyMBiODcxJ9mxWIMbBWeDFwCplbN7Ku7YmGw1QMUIAA))

```js
type Name =
  | "Simba"
  | "Mufasa"
  | "Nala"
  | "Sarabi"
  | "Sarafina"
  | "Scar"
  | "Kiara"
  | "Kovu"
  | "Vitani";

const GENDER = {
  MALE: "male",
  FEMALE: "female"
};

const purrs = {
  brief: "prr",
  normal: "prrr",
  long: "prrrrr",
  insane: "prrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrr"
};

type Kitten = {| // recommend using sealed and exact objects

  /** basic fields */
  
  name1: string,
  name2: // disjoint union for more refined typing
    | "Simba"
    | "Mufasa"
    | "Nala"
    | "Sarabi"
    | "Sarafina"
    | "Scar"
    | "Kiara"
    | "Kovu"
    | "Vitani",
  name3: Name, // type alias for easier reuse and readability
  
  age: number,
  
  gender: $Values<typeof GENDER>, // 'male' | 'female'
  
  purrs: $Keys<typeof purrs>, // 'brief' | 'normal' | 'long' | 'insane'

  /** function fields */
  
  purr1: Function, // not recommended because Function is now aliased to `any`
  purr2: () => {}, // likely a typo, did you mean () => void?

  purr3: () => void, // (very common) a function that doesn't take nor return anything
  purr4: string => void, // (very common)
  purr5: (name: string) => boolean, // (very common) use named parameter for better readability

  /** object fields */
  mane1: Object, // not recommended
  mane2: {}, // not recommended: not even sealed, nearly the same as any
  mane3?: { // optional field, meaning this field may or may not exist
    [key: string]: any // can be a last resort if you really don't know what's going on
  },
  
  mane4: ?{ // nullable, meaning this field can be null or undefined
    color: string, // (very common) with defined properties
    type: "mane" | "beard" | "mustache"
  },
  
  manes?: ?({ // fields can be both optional and nullable
    color: string,
    type: "mane" | "beard" | "mustache"
  }[]) // array of objects
|};

const kitten: Kitten = {
  name1: 'kitten',
  name2: 'Simba',
  name3: 'Nala',
  age: 7,
  gender: 'male', // note that this type is widened
  purrs: 'brief', // must be one of the literals
  purr1: () => { console.log('prr') },
  purr2: () => ({}),
  purr3: () => { console.log('prr') },
  purr4: name => { console.log(name + ', prrrrr') },
  purr5: name => !!name,
  mane1: {},
  mane2: {},
  mane3: { color: 'darkbrown' },
  mane4: { color: 'darkbrown', type: 'beard' },
  manes: [{ color: 'darkbrown', type: 'mustache' }]
};
```


### Functions

[https://flow.org/en/docs/types/functions/](https://flow.org/en/docs/types/functions/)

The docs cover basics of functions such as:

- [Function parameters (input) and return value (output) are often optional](https://flow.org/en/docs/types/functions/)
- There are three different syntaxes to annotate functions: [function declarations](https://flow.org/en/docs/types/functions/#toc-function-declarations)﻿, [arrow functions](https://flow.org/en/docs/types/functions/#toc-arrow-functions)﻿, and [function types](https://flow.org/en/docs/types/functions/#toc-function-types)
- Syntaxes for annotating [function parameters](https://flow.org/en/docs/types/functions/#toc-function-parameters)﻿, [optional parameters](https://flow.org/en/docs/types/functions/#toc-optional-parameters)﻿, and [rest parameters](https://flow.org/en/docs/types/functions/#toc-rest-parameters)
- [Return types ensure that every branch of your function returns the same type](https://flow.org/en/docs/types/functions/#toc-rest-parameters)
- [What is a *predicate function*?](https://flow.org/en/docs/types/functions/#toc-predicate-functions)
- `[Function` is now aliased to `any`](https://flow.org/en/docs/types/functions/#toc-function-type) ﻿and is therefore not recommended

**Examples** ([Flow Try](https://flow.org/try/#0FAegVGAEBmCuB2BjALgSwPbwM6QO6uQAtJ51IAHAQwCdKBbAU2Qep1Osmqdmu0jBDBgcJGkwUe1AIwAKAJQAuSADd0qACaQA3pEggQMBCgzxI6hogA2NSmPjBdiTFnSWGAOkvoA5jIDk5JJ+cgDcwAC+wE7YyBLU1ABMkAC8kPJKqhopAHzauvqQNNTouIaiJg6Q0S5unj7+gfHBYZHIAJ7kDJAACpIAgilpcjkqauph1bGN1ADMSr3xA6nyI1qV1a4eXr4BQaERQuBQIsbOeATEVLSMzKyF8JoG6BxcyDx8AkIndnHUACwyeD0BhKLDIaioeDeRSQMEQqHaSqvd6QPyEBiWLwAGlRkAA1CRgS0hJNfgBWQaA4Gg8GQ6E0+HeVZI7i8VHozHoHF+fGExjE4DtTo9SQAIUGcLpI0lUJC+QMbXQsEgdEobUg6HIdkomPVbkoyi6SqmNhuLD5DCwUWcU0kADYFAtqOLUkDGCM0RjsbiCW6GGFQBAKK42nRnuRCKhEGVTnwDN4GPAWFGcJ9viZfn1kAAeAAqSh0foZUvC2RkiC4th4IMguZhMqZa10yLZns53N5FYYVa47j9AoK0yzMkLwJrflghEnPPCoT0BjBUYA1uqlww2gAjdA0TQsYrUQ5B9NnfBEWHIWwp-iCQUdLpOgCyDDDgybVUoiHR6gActTz4ysUqKlGGLKF61pKEcQKRAdWsDc3FhVBvCBN4uAOUlpifMN5kkLCyGWIt-zpYZklyN9UGgNIAEJMOfdB3Bgz8GB-YFhjfXRaLDBiPy-X93VdIlKkiZtWVMTj6MY3jBMiQMoHQQ1qC8Sh1ClT5b2FJ0AHULizNA3nMHBUjfdIiMgoDCIbcCAPMv8GxxNBGCwJR4FgOgNxYKy6UAyIMMkbSiF0ghYAMnD4n8whAv0y1KT9AB+UDvHs1BHPikhXPc6gSLIyoKOov02MqETUNMPxSEgDkvD8MJdHCSAMSwLpcpkKiHMtArdCKlE229HlfUEmq6ssBrEQ6yA3FiJwEFiVIAAYcW8LgmClVJuvQKrCrwSMEPLJV4FibNIFarB2tGqpduQPE8Wq06FoYJaETxFbyq9NbrpqjaW1MW77qZAk-A7Pr+SEiIgA))

```js
/** functions with no parameters nor returns */

function purr1(): void {  // function declaration
  console.log('purr');
}
const purr2 = (): void => {  // arrow function
  console.log('purr');
}
type PurrA = () => void;
const purr3: PurrA = () => {
  console.log('purr');
}

/** functions with parameters and / or returns */

function purr4(name: string): string {
  return 'hello, ' + name;
}

const purr5 = (name: string): string => {
  return 'hello, ' + name;
}

type PurrB = string => string;  // you may optionally leave out parameter names
const purr6:PurrB = name => 'hello, ' + name;

/** polymorphic functions / generics */
function purrAt<T: { name: string }>(creature: T): string {
  return 'hello, ' + creature.name;
}

purrAt({ namee: 'uhuh' }); // sticky keyboard error

/** functions with statics */

type PurrMemo = {
  cachedName: string,
  [[call]](name: string): string, // callable signature
}
const purrMemo: PurrMemo = (name: string) => {
  if (!purrMemo.cachedName) {
    purrMemo.cachedName = name;
  }
  return purrMemo.cachedName;
}

/** overloading */

type PurrWithAttitudes = {
  (): string,
  (name: string): string,
  (name: string, times: number): string,
}
const purrWithAttitudes: PurrWithAttitudes = (name?: string, times?: number) => {
  if (!name) {
    return 'no hello';
  } else if (!times) {
    return 'hello, ' + name;
  } else {
    let count = 0, greeting = 'hello';
    while (count < times) {
      count++;
      greeting += ' hello';
    }
    return greeting + ', ' + name;
  }
}`
```


## More Notes
<!-- TODO: reorganize the following -->

- Basics
  - [Exact v.s. sealed](./basics/exact-vs-sealed.md)
- React
  - [React component types](./react/react-component-types.md)
  - [`React.memo`](./react/react-memo.md)
  - [`React.lazy`](./react/react-lazy.md)
  - [Higher order components](./react/annotating-higher-order-components.md)
  - [Connected components by React Redux](./react/annotating-connected-components.md)
- Advanced
  - [Callable properties and function statics](./advanced/callable-properties-and-function-statics.md)



## Try Flow bookmarklets

- [`React.Config` use case](https://flow.org/try/#0PQKgBAAgZgNg9gdzCYAoAlgWwA5wE4AuyYAhgM5gBKApiQMZFR5yZgDketDbA3KvwQCe2amACyggMItcAO2qyCABWbYKAXjABvVGFIAuMGQJ50sgOYAaXWABGh2QFdMt6nmt66h23DgxastYAvnx0cLLG4lIy4QpEmgAU2KpkhhLSOLGKKnBqAJRg6gB8YAA8ACboAG5FNlrJuWQAdCRBdQ1qTbZtevUpTXRtpcCVNXz8UI6yDOjhYAjoBAAWAGokpiQEsxGlSoZaQZZgK-tBRQk2AOp4JNgi5RlycYY09ARNAIK2xjcMj1kEXa1PKGFaFEqvBifb4mN7-eSKUoAEgAIugoFBdkcVkUSjo9JwCI48LIwAkqut0Jttjk1KCCsUbHpJtMtnN4XFLotVpTqeEyEkUoYlAV8XpxYTiaTStdbvcOYptE1lR0yEElcqKRs2bJaWqwMAinxxWAQqg2qgwhEiOkYgiCFzlh9CvNuWttdsyKVbZl7XqjloSIYfmZzGcEj6noo8glA4Y2EtqDB4GwgnlxtQAB64QhgcrUKAkRwwIgJBklCrVWoASG90V9nO5zpI6gARLI4ERE8m4K27OotABGACs6roA8LMDI1HVhtQw1GRSAA)
- [Annotating memoized factorial function](https://flow.org/try/#0PTAEAEDMBsHsHcBQiAuBPADgU1AWSwLawCWAXlgCYBiAhgMYqwBOxN0AKpjgLygDeiUKDr0AFlgBc-QaACQAbQB2AVwIAjLEwC6Ules0yAvgBoZ8+SOjQtWgBR6NTAJS7Vj04eR1YigM4pQSHpGFjYpfCIySloGZlYOLlBeRSSAPmkhYkhQWwBCINjQ6AA6ETpxJwyhQOC4tlKxHn5PIRbQLJyCkPiG8qwlLVBc7l5lRQosSGJFSkqBatAmLBRlJhSuupKy8QGjGQ2i3p3FQeSkkdAABlAAflAARlBdUAAqGsL4+1AAWgenGSWKzW7269W2-ROiEMQA)
- [Cannot write overloaded function bodies](https://flow.org/try/#0KYDwDg9gTgLgBAMwK4DsDGMCWEVwO6YwAWAggBR4CGKMAziQFxy0xSYoDmAlHAN4BQcOJgRwK1OiTgBeWXADkleTyjAYSKLkXyA3ILjAANrWBxV6zYkrHgegL79+aHCziUA8lABi1k0xZsnDL4hKRk2lw6QA)
- [Cannot call function that takes a refined type even if the extra field is optional](https://flow.org/try/#0C4TwDgpgBAksEFsoF4oG8A+AoKUCWAJgFxQB2ArggEYQBOANDmQIYIQkDOwtepA5owwBfLFlCRY8BAHU8wABYARCBwDGPMMDwB7UinRMAdMYAkAUQAezVcAA8cRAD5GuANQEV6vJp2kA-JzcvHxYIlgAZuSkNr5QwMwA1ioOCAAUcogkKQCUBriquhzaADYQhsXafOlS2QDcTPFJHCmyCspqGlq61Yh1oaKR0V16jclSrUqenb49CFnjcpMd3sO5aEwFpEWl5ZWzfUJAA)
- [Cannot properly refine "T or generates T" type](https://flow.org/try/#0C4TwDgpgBAKg8gJwOIQHYQQQ2BAzjAHhgD4oBeKACkoEpzSY6AfWAbgCh2AzAV1QGNgASwD2qKMEwBrPIhTosOXHC4xwEIuuKVgALlhy0GbHkJrIxOgG92UKEK5VQkEY+DkyFAOS8BwsV7WtnZQ-GK4IgA2EAB0kSIA5jq0NBx2AL5QEJG40DYhoeFRsfFJwKnB6ezpQA)
- [Spread v.s. &](https://flow.org/try/#0PQ0gEDyAuAWCmAnAzuAZgSwDbwFDQE8AHecAQXAF5wBvXccAQwC4mA7AgGlwF8BuXPmKkAQlXLgAZLXrgARq0Ydu-WbjBhwAWQLpseQiXABhcWOl0GAY0XLeA3GgCubK9AwB7NuAAqACktwK24GADpwokQPImReVmMAShkGSOjkULleXCA) @nutstick

## Other resources

- [typescript-vs-flowtype](https://github.com/niieani/typescript-vs-flowtype/)

### Guides

- Upgrading Flow past 0.85, annotating connect
  - [Asking for Required Annotations](https://medium.com/flow-type/asking-for-required-annotations-64d4f9c1edf8)
  - [Quick Note Fixing `connect` FlowType Annotation after 0.89](https://dev.to/wgao19/quick-note-fixing-connect-flowtype-annotation-after-089-joi)
  - [Ville's and Jordan Brown's guide: _Adding Type Parameters to Connect_](https://gist.github.com/jbrown215/f425203ef30fdc8a28c213b90ba7a794)

### Books

- [Programming TypeScript](https://www.oreilly.com/library/view/programming-typescript/9781492037644/) A practical handbook on TypeScript that also explains the whys and hows behind static type checking well, see also [swyx](https://twitter.com/swyx)'s recommendation [tweet](https://twitter.com/swyx/status/1135525665971695617)

## Contributing

[Questions](https://github.com/wgao19/flow-notes/issues/new?assignees=&labels=question&template=question.md) are always welcome!

Currently, I am still in the process of organizing my notes, after setting up an initial structure I'd like to invite more people to learn and share together.
