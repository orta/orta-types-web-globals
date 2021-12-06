A version of [@types/web](https://www.npmjs.com/package/@types/web) which has the types separated from the declaration of globals based on [this diff](https://github.com/microsoft/TypeScript-DOM-lib-generator/pull/new/split_types_2) with a bit of manual hand-holding by me.

Based on discussion in [microsoft/TypeScript#43972](https://github.com/microsoft/TypeScript/issues/43972#issuecomment-919403670).

Old:

```ts
var EventTarget: {
    prototype: EventTarget;
    new(): EventTarget;
};
```

Now:
```ts
interface EventTargetConstructor {
    prototype: EventTarget;
    new(): EventTarget;
}

var EventTarget: EventTargetConstructor
```

This library can be used like:

```sh
pnpm add @typescript/lib-dom@npm:@orta/lib-dom-globals --save-dev
npm install @typescript/lib-dom@npm:@orta/lib-dom-globals --save-dev
yarn add @typescript/lib-dom@npm:@orta/lib-dom-globals --dev
```


Which will give other projects like node/deno etc the ability to do:

```
/// <reference lib="dom.types" />
```

Which resolves to [`./types.d.ts`](./types.d.ts) - which only contains the global type and no runtime declarations.
