<template>
  <div>
    <h1>tsxからVueとReact向けにビルドする</h1>
  </div>
  <ul>
    <li class="text-size-xl text-dark">
      jsx は、それをビルドするツールによって異なる関数へ置き換えられる糖衣構文。
    </li>
    <li class="text-size-xl text-dark">
      React では React.createElement、Vue では hに変換される。
    </li>
    <li class="text-size-xl">state を持たせるにはランタイムが必要</li>
  </ul>
  <div>
    <p class="text-size-xl">
      state を持たせると React か Vue のランタイムに依存してしまう。
    </p>
    <p class="text-size-xl">
      言い換えれば、state を持たなければ、どちらでも使えるコンポーネントになる。
    </p>
  </div>
</template>
