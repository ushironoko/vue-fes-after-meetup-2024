---
# You can also start simply with 'default'

# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: 1つのtsxからVueとReact向けにビルドする
info: |
  ## 1つのtsxからVueとReact向けにビルドする
# apply unocss classes to the current slide
class: text-white
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: view-transition
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# take snapshot for each slide in the overview
overviewSnapshots: true
---

# 1つのtsxからVueとReact向けにビルドする

STORES 株式会社 / ushironoko

---

## 話すこと

  <br>

- tsx
- VueとReact
- ビルド

  <br>

<style>
* {
  font-size: 36px;
}

h2 {
  font-size: 48px;
}
</style>

---

<div>
  <Page3n1 />
</div>

---

<div>
  <Page3n2 />
</div>

---

<Page5n1 />

<br>

これは

```tsx
export default () => <>Hello, World!</>;
```

こういう型になる

```tsx
() => JSX.Element;
```

---

<Page6 />

```tsx
export default ({ text }: { text: string }) => <>Hello, {text}!</>;
```

<br>

```tsx
({ text }: { text: string }) => JSX.Element;
```

---

<Page7 />

<br>

```tsx
const value = state("world!"); // state を持つにはUIライブラリの力が必要

export default () => <>Hello, {value}!</>;
```

<br>

副作用のある関数は、その作用をトリガーとして再レンダリングされなければならない。

stateの追跡やスケジューリング等、高度な機能が必要になるが、tsx はただのテンプレートなのでその機能は提供していない。

---

<Page8 />

---

<Page3n1 />

---

<Page10/>

---

<Page11/>

```tsx
import { useState } from "react";

const HelloWorld = () => {
  const [text, setText] = useState("Hello");

  return <button onClick={() => setText("こんにちは！")}>{text} World!</button>;
};

export default HelloWorld;
```

---

<Page12/>

<br>

このコードは上記のコマンドでビルドすると

```tsx
const HelloWorld = () => <div>Hello World!</div>;
```

こうなる

```tsx
const HelloWorld = () => React.createElement("div", null, "Hello World!");
```

---

<Page13 jsx="react-jsx" hasTitle/>

jsx runtimeをバンドルに埋め込み、依存を内部化する。

```tsx
const HelloWorld = () => jsxRuntimeExports.jsx("div", null, "Hello World!");
```

<Page13 jsx="preserve" factory="h" />

jsx コードをそのまま残し、指定された関数に置き換える。jsx の解釈を tsc が他のビルドツールに委ねた状態。

```tsx
const HelloWorld = () => h("div", null, "Hello World!");
```

React では jsx 構文は最終的に `createElement` という関数に置き換わるが、

オプションを組み合わせることで、ビルド後の jsx 構文を誰に・どのように解釈させるか指示できる。

---

<Page14 />

```tsx
const App = () => <div>Hello World!</div>;
```

```ts
import { defineComponent } from 'vue';

const App = defineComponent({
  setup() {
    return () => (
      <div>Hello World!</div>
    );
  },
});
```

```ts
h("div", null, "Hello World!"); // return VNode
```

---

<div class="mt-36">
<p>さっき見ましたね？</p>

```ts
h("div", null, "Hello World!"); // return VNode
```

</div>

---

<Page16 />

---

<Page17 />

---

<Page18 />

---

<Page19 />

---

<Page20 />

---

<Page21n1 />

<br>

---

<Page21n2 />

<br>

この部分さえ守っていれば、関数コンポーネントとして認識される。

---

<Page22 />

```tsx
type Props = {
  liProps: { title: string; url: string }[];
  notificationEl: () => JSX.Element;
};
const Navigation = ({ liProps, notificationEl }: Props) => {
  return (
    <nav className="...">
      <ul>
        {liProps.map(({ title, url }) => (
          <li className="...">
            <a href={url}>{title}</a>
          </li>
        ))}
        <li>{notificationEl()}</li>
      </ul>
    </nav>
  );
};

export default Navigation;
```

---

<Page23 />

---

<Page24 />

```ts
import { defineBuildConfig } from "unbuild";

export default defineBuildConfig([
  {
    // rollup で React 向けにビルドする
    entries: [
      { input: "Navigation.tsx", name: "Navigation.react", outDir: "dist/" },
    ],
  },
  {
    // rollup で Vue 向けにビルドする
    entries: [
      { input: "Navigation.tsx", name: "Navigation.vue", outDir: "dist/" },
    ],
  },
]);
```

しかし、これだけではまだ動かない。

<style>
pre {
  height: 260px;
}
</style>

---

<Page25 />

---

<Page26 />

```ts
entries: [
  {
    // ...省略
    rollup: {
      esbuild: {
        tsconfigRaw: {
          compilerOptions: {
            jsx: "preserve", // jsx コードをそのまま残す
            jsxFactory: "h", // h 関数を使うことを指示
          },
        },
      },
    },
  },
],
```

---

<Page27 />

```ts
entries: [
  {
    // ...省略
    rollup: {
      esbuild: {
        jsx: "automatic"
      },
    },
  },
],
```

しかし、まだこれだけでは動かない。

---

<Page28 />

```ts
// dist/Navigation.vue.mjs
const Navigation = ({ l, n }) => {
  // h は元のコードに含まれていない
  return h(
    "nav",
    { className: "..." },
    h(
      "ul",
      { className: "..." },
      l.map(/** なんやかんや */),
      h("li", null, n()),
    ),
  );
};

export { Navigation };
```

---

<Page29 />

```ts
import { jsx, jsxs } from "xxx/jsx-runtime";
```

<br>

Vue はこう。

```ts
import { h } from "vue";
```

というわけで、自分でビルド結果に import 文を追加する。

---

<Page31 />

---

<Page32 />

```ts
import { parseModule, loadFile, writeFile } from "magicast";
import { exit } from "node:process";
import path from "node:path";
import { fileURLToPath } from "node:url";

const MODULE_PATH = path.join(
  path.dirname(fileURLToPath(import.meta.url)),
  `/../dist/Navigation.vue.mjs`,
);

const run = async () => {
  const mod = await loadFile(MODULE_PATH);
  // 元のコードの先頭に import 文を追加し、再度モジュールに変換する
  const result = parseModule(`import { h } from "vue";\n${mod.$code}`);
  return await writeFile(result, MODULE_PATH);
};

await run();
```

しかし、まだこれだけでは動かない。

---

<Page33 />

```ts
// dist/Navigation.vue.mjs
const Navigation = ({ l, n }) => {
  // h は元のコードに含まれていない
  return h(
    "nav",
    { className: "..." }, // 👈
    h(
      "ul",
      { className: "..." }, // 👈
      l.map(/** なんやかんや */),
      h("li", null, n()),
    ),
  );
};

export { Navigation };
```

React と Vue では class/className の差分がある。元の定義は className にしているので、ここでも Vue 向けの変換を行う。

---

<Page34 />

```ts
import { parseModule, loadFile, writeFile } from "magicast";
import { exit } from "node:process";
import path from "node:path";
import { fileURLToPath } from "node:url";

const MODULE_PATH = path.join(
  path.dirname(fileURLToPath(import.meta.url)),
  `/../dist/Navigation.vue.mjs`,
);

const run = async () => {
  const mod = await loadFile(MODULE_PATH);
  const result = parseModule(mod.$code.replaceAll(" className:", " class:"));
  return await writeFile(result, MODULE_PATH);
};

await run();
```

ここまでやると動きます。

---

<Page35 />

---

<Page36 />

```tsx
type Props = {
  notificationEl: () => JSX.Element;
};
const Navigation = ({ notificationEl }: Props) => {
  return (
    <nav className="...">
      <ul>
        // ...省略
        <li>{notificationEl()}</li> // 👈 これは React でも Vue でも有効
      </ul>
    </nav>
  );
};
```

---

<Page37 />

App.vue

```tsx
import "vue/jsx";
```

```tsx
type Props = {
  notificationEl: () => JSX.Element; // 👈 これが有効になる
};
const Navigation = ({ notificationEl }: Props) => {
  return (
    <nav className="...">
      <ul>
        // ...省略
        <li>{notificationEl()}</li>
      </ul>
    </nav>
  );
};
```

---

<Page38 />

---

<Page39 />

tsconfig.react.json

```json
{
  "compilerOptions": {
    /** 色々省略 */
    "jsx": "preserve",
    "jsxFactory": "createElement",
    "noEmit": true,
    "emitDeclarationOnly": true,
    "declaration": true
  }
}
```

tsconfig.vue.json

```json
{
  "compilerOptions": {
    /** 色々省略 */
    "jsx": "preserve",
    "jsxFactory": "h",
    "noEmit": true,
    "emitDeclarationOnly": true,
    "declaration": true
  }
}
```

<style>
pre {
  height: 100px;
}
</style>

---

<Page40 />

unbuild.config.ts

```ts
import { defineBuildConfig } from "unbuild";

export default defineBuildConfig([
  // Build for React
  {
    entries: [
      // ...省略
    ],
    failOnWarn: false, // 👈　これがないとビルドが壊れる
    declaration: true, // 👈　React 向けの型定義ファイルが生成される
    rollup: {
      dts: {
        tsconfig: "tsconfig.react.json",
      },
      // ...省略
    },
  },
  // Build for Vue
  {
    entries: [
      // ...省略
    ],
    failOnWarn: false, // 👈　これがないとビルドが壊れる
    declaration: true, // 👈　Vue 向けの型定義ファイルが生成される
    rollup: {
      dts: {
        tsconfig: "tsconfig.vue.json",
      },
      // ...省略
    },
  },
]);
```

<style>
pre {
  height: 300px;
}
</style>

---

<Page41 />
