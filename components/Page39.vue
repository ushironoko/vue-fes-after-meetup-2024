<template>
  <div>
    <h1>おまけ: 型を吐く</h1>
  </div>
  <div>
    <p class="text-size-lg">
      unbuild の rollup オプションは dts 出力するための拡張もできる。
    </p>
    <p class="text-size-lg">
      そのままでは動かないため、React/Vue それぞれのビルド向けの tsconfig
      を作って渡す。esbuild
      に渡されるオプションとは別になるので注意（実態と違うが jsx: preserve
      にしないと通らない）。
    </p>
  </div>
</template>
