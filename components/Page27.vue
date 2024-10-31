<template>
  <div>
    <h1>tsxからVueとReact向けにビルドする</h1>
  </div>
  <div>
    <p class="text-size-xl">
      <span class="text-amber text-size-2xl">unjs/unbuild</span>
    </p>

    <p class="text-size-xl">
      React の場合は、esbuild にある jsx オプション（tscのオプションではない）に
      <span class="text-cyan">automatic</span>
      を指定することでいい感じにビルドしてくれる。<span class="text-size-sm"
        ><a
          target="_blank"
          href="https://esbuild.github.io/content-types/#auto-import-for-jsx"
          >auto-import-for-jsx | esbuild</a
        ></span
      >
    </p>

    <p class="text-size-xl">
      実際には
      <span class="text-cyan">automatic</span> オプションを指定した場合、
      <span
        class="px-1 text-amber border border-solid border-amber rounded text-size-lg"
        >tsc --jsx react-jsx</span
      >と同等の出力結果になる。
    </p>
  </div>
</template>
