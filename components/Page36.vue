<template>
  <div>
    <h1>tsxからVueとReact向けにビルドする</h1>
  </div>
  <div>
    <p class="text-size-lg">Q. slot はどうするの？</p>
    <p class="text-size-lg">A. render prop で代用する</p>
    <p class="text-size-lg">
      slot を React で同等の機能に変換するのはコストが高い。render prop
      ならランタイムを問わず動作するので、こちらに寄せる方が良い。
    </p>
  </div>
</template>
