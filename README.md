# Angular / TypeScript projects style guide


**TypeScript + ESLint**

- [Require that member overloads be consecutive](#rules-for-eslint)
- [Awesome Interviews](https://github.com/alex/what-happens-when)
- [Angular Interview Questions](https://github.com/sudheerj/angular-interview-questions)


---

## TypeScript + ESLint 

- https://github.com/typescript-eslint/typescript-eslint

### Require that member overloads be consecutive <a id="rules-for-eslint"></a>

Use `'@typescript-eslint/adjacent-overload-signatures': 'error'`, because grouping overloaded members together can improve readability of the code. 

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
