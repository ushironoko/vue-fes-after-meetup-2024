<template>
  <div>
    <h1>Vue固有の問題まとめ</h1>
  </div>
  <ul>
    <li class="text-size-xl">
      esbuild のオプションで tsconfig を拡張し、<span class="text-amber"
        >jsx: "preserve"</span
      >、<span class="text-amber">jsxFactory: "h"</span>
      を設定する
    </li>
    <li class="text-size-xl">
      <span class="text-cyan">h</span> が参照エラーにならないようにビルド結果に
      <span class="text-amber">{{ `import { h } from "vue";` }}</span>
      を追加する
    </li>
    <li class="text-size-xl">
      元コードが className を用いている場合は、class に変換する
    </li>
  </ul>
</template>
