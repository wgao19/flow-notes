# Flow Notes

📝 Notes on using and understanding Flow, starting from version 0.85.

🚧 This repo is a work in progress.

- [Umbrella issue](https://github.com/wgao19/flow-notes/issues/1)

## Contributing

[Questions](https://github.com/wgao19/flow-notes/issues/new?assignees=&labels=question&template=question.md) are always welcome!

Currently, I am still in the process of organizing my notes, after setting up an initial structure I'd like to invite more people to learn and share together.

## Notes

### Basic Concepts

https://flow.org/en/docs/lang/

Basic type examples

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
  
  gender: $values<GENDER>, // 'male' | 'female'
  
  purrs: $keys<typeof purrs>, // 'brief' | 'normal' | 'long' | 'insane'

  /** function fields */
  
  purr1: Function, // not recommended because parameters and returns are not restricted
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
```

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
