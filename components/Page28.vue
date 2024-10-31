<template>
  <div>
    <h1>Vue固有の問題</h1>
  </div>
  <div>
    <p class="text-size-xl">
      <span class="text-amber text-size-2xl">unjs/unbuild</span>
    </p>

    <p class="text-size-xl">
      Vue向けビルド では jsx は h 関数を使うように変換されるが、元コードに h
      関数をインポートするコードは含まれていないため、このままでは参照エラーになる。
    </p>
  </div>
</template>
