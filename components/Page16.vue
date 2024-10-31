<template>
  <div>
    <h1><span class="text-cyan">j(t)sx</span>の正体</h1>
  </div>
  <ul>
    <li class="text-size-xl">
      jsx は、それをビルドするツールによって異なる関数へ置き換えられる糖衣構文。
    </li>
    <li class="text-size-xl">React では React.createElement、Vue では h。</li>
    <li class="text-size-xl">tsc でも、そうでないツールでもビルドされうる。</li>
    <li class="text-size-xl">
      tsc は tsc でビルドしない時のためのオプションを提供している。
    </li>
  </ul>
</template>
