# Angular / TypeScript projects style guide

**TypeScript + ESLint**

-   [Require that member overloads be consecutive](#rules-for-eslint)
-   [Requires using either `T[]` or `Array<T>` for arrays](#array-types)
-   [Disallows awaiting a value that is not a Thenable](#await-thenable)
-   [Requires type annotations to exist (typedef)](#typedef)
-   [Require explicit return and argument types on exported functions' and classes' public class methods](#explicit-module-boundary-types)

---

## TypeScript + ESLint

-   https://github.com/typescript-eslint/typescript-eslint

### Require that member overloads be consecutive <a id="rules-for-eslint"></a>

Use
[`'@typescript-eslint/adjacent-overload-signatures': 'error'`](https://github.com/typescript-eslint/typescript-eslint/blob/master/packages/eslint-plugin/docs/rules/adjacent-overload-signatures.md),
because grouping overloaded members together can improve readability of the code.

![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) `Bad pattern`

```ts
class Foo {
    foo(s: string): void;
    foo(n: number): void;
    bar(): void {}
    foo(sn: string | number): void {}
}

export function foo(s: string): void;
export function foo(n: number): void;
export function bar(): void;
export function foo(sn: string | number): void;
```

![#c5f015](https://via.placeholder.com/15/c5f015/000000?text=+) `Good pattern`

```ts
class Foo {
    foo(s: string): void;
    foo(n: number): void;
    foo(sn: string | number): void {}
    bar(): void {}
}

export function bar(): void;
export function foo(s: string): void;
export function foo(n: number): void;
export function foo(sn: string | number): void;
```

### Requires using either `T[]` or `Array<T>` for arrays <a id="array-types"></a>

Use
[`'@typescript-eslint/array-type': 'error'`](https://github.com/typescript-eslint/typescript-eslint/blob/master/packages/eslint-plugin/docs/rules/array-type.md)
for always using `T[]` or readonly `T[]` for all array types.

![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) `Bad pattern`

```ts
const x: Array<string> = ['a', 'b'];
const y: ReadonlyArray<string> = ['a', 'b'];
```

![#c5f015](https://via.placeholder.com/15/c5f015/000000?text=+) `Good pattern`

```ts
const x: string[] = ['a', 'b'];
const y: readonly string[] = ['a', 'b'];
```

### Disallows awaiting a value that is not a Thenable <a id="await-thenable"></a>

Use
[`'@typescript-eslint/await-thenable': 'error'`](https://github.com/typescript-eslint/typescript-eslint/blob/master/packages/eslint-plugin/docs/rules/await-thenable.md)

![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) `Bad pattern`

```ts
await 'value';

const createValue = () => 'value';
await createValue();
```

![#c5f015](https://via.placeholder.com/15/c5f015/000000?text=+) `Good pattern`

```ts
await Promise.resolve('value');

const createValue = async () => 'value';
await createValue();
```

### Requires type annotations to exist <a id="typedef"></a>

Many believe that requiring type annotations unnecessarily can be cumbersome to maintain and generally reduces code
readability. TypeScript is often better at inferring types than easily written type annotations would allow. And many
people believe instead of enabling typedef, it is generally recommended using the `--noImplicitAny` and
`--strictPropertyInitialization` compiler options to enforce type annotations only when useful. This rule can enforce
type annotations in locations regardless of whether they're required.

But why is annotation description useful? Because for the code review, you will not be able to find out what will change
in runtime due to inferred types. But when you specify types, you know exactly what to change to:

![](https://habrastorage.org/webt/3x/q6/ds/3xq6dsrygwwblzl2ntfdpd_wkw8.gif)

It is also worth noting that if we do not use type annotations for methods, it may be difficult for us to read the code
during the review, we may not notice something and not pay attention to how the data type has changed if the build does
not crash with an error.

![](https://habrastorage.org/webt/du/sc/qv/duscqvjgqnaelbkcfmjf2myhhty.gif)

Reference to [explicit-module-boundary-types](#explicit-module-boundary-types)

# Require explicit return and argument types on exported functions' and classes' public class methods <a id="explicit-module-boundary-types"></a>

Explicit types for function return values and arguments makes it clear to any calling code what is the module boundary's
input and output.

![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) `Bad pattern`

```ts
// Should indicate that a number is returned
export function myFn() {
    return 1;
}
```

![#c5f015](https://via.placeholder.com/15/c5f015/000000?text=+) `Good pattern`

```ts
// A return value of type number
export function myFn(): number {
    return 1;
};
```
