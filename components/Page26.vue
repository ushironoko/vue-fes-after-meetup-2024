<template>
  <div>
    <h1>tsxからVueとReact向けにビルドする</h1>
  </div>
  <div>
    <p class="text-size-xl">
      <span class="text-amber text-size-2xl">unjs/unbuild</span>
    </p>

    <p class="text-size-xl">
      デフォルトの設定では、jsx をどう解釈するのかは定義されていない。unbuild
      は内部的に esbuild を用いて jsx をコンパイルするため、esbuild
      オプションを渡せるようになっている。
    </p>

    <p class="text-size-xl">
      esbuild のオプションに Vue 用の設定を渡すことで、Vue
      用のコードとしてビルドすることができる。
    </p>
  </div>
</template>
