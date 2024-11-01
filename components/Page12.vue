<template>
  <div>
    <h1><span class="text-cyan">React</span>における<span class="text-cyan">tsx</span></h1>
  </div>
  <div>
    <p class="text-size-xl">
      React は独自のテンプレートをもたないが、独自の解釈でtsxを扱っている。
    </p>
    <p class="text-size-xl">
      こうすることで、React18 における Form Action のような機能を実現している。
    </p>
    <p class="pl-6 text-size-sm">
      <code>{{ `<form action={serverAction}>` }}</code>
    </p>
    <p class="pl-6 text-size-sm">
      通常 form の action 属性に関数を渡すことはできないが、React では可能。
    </p>
    <p class="text-size-xl">
      TypeScript は Reactの jsx とそれ以外を区別しており、<span class="px-1 text-amber border border-solid border-amber rounded text-size-lg">tsc</span>
      でビルドする際の結果に影響する。
    </p>
    <p class="text-size-xl">例えば <span class="px-1 text-amber border border-solid border-amber rounded text-size-lg">tsc --jsx react</span> でビルドすると、React の runtime で jsx を解釈するコードが生成される。
    </p>
  </div>
</template>
