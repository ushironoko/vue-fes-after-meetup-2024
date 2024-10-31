<template>
  <div>
    <h1>
      <span class="text-cyan">Vue</span>における<span class="text-cyan"
        >tsx</span
      >
    </h1>
  </div>
  <div>
    <p class="text-size-xl">
      Vue は独自のテンプレートを持っているが、tsx を用いることもでき、変換には
      Babel のプラグインを用いている。<a
        class="text-size-sm"
        target="_blank"
        href="https://ja.vuejs.org/guide/extras/render-function"
        >レンダー関数とJSX</a
      >
    </p>
    <p class="text-size-xl">
      Vue コンポーネントで tsx を記述した場合、それは VNode
      を生成するレンダー関数 <span class="text-cyan">h</span>
      に置き換わる。様々な構文に対応しており、以下はその一部。
    </p>
  </div>
</template>
