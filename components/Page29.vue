<template>
  <div>
    <h1>Vue固有の問題</h1>
  </div>
  <div>
    <p class="text-size-xl">
      <span class="text-amber text-size-2xl">unjs/unbuild</span>
    </p>

    <p class="text-size-xl">Q. jsxImportSource は？</p>
    <p class="text-size-xl">
      A. esbuild が<a
        target="_blank"
        href="https://github.com/evanw/esbuild/issues/718"
        >対応していない</a
      >。
    </p>
    <p class="text-size-xl">
      かつ、jsxImportSource は以下のような export を要求しており、Vue は root
      から直接 h を import する形式なので使えない。
    </p>
  </div>
</template>
