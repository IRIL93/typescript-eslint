# Disallows calling an any type value (`no-unsafe-call`)

Despite your best intentions, the `any` type can sometimes leak into your codebase.
Member access on `any` typed variables is not checked at all by TypeScript, so it creates a potential safety hole, and source of bugs in your codebase.

## Rule Details

This rule disallows calling any variable that is typed as `any`.

Examples of **incorrect** code for this rule:

```ts
declare const anyVar: any;
declare const nestedAny: { prop: any };

anyVar();
anyVar.a.b();

nestedAny.prop();
nestedAny.prop['a']();

new anyVar();
new nestedAny.prop();

anyVar`foo`;
nestedAny.prop`foo`;
```

Examples of **correct** code for this rule:

```ts
declare const properlyTyped: { prop: { a: () => void } };

nestedAny.prop.a();

(() => {})();

new Map();

String.raw`foo`;
```

## Related to

- [`no-explicit-any`](./no-explicit-any.md)
- TSLint: [`no-unsafe-any`](https://palantir.github.io/tslint/rules/no-unsafe-any/)
