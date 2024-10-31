<script setup lang="ts">
defineProps({
  hasTitle: Boolean,
  jsx: String,
  factory: String,
});
</script>

<template>
  <div>
    <template v-if="hasTitle"
      ><h1>
        <span class="text-cyan">React</span>における<span class="text-cyan"
          >tsx</span
        >
      </h1></template
    >
  </div>
  <div>
    <p class="text-size-xl">
      <span
        class="px-1 text-amber border border-solid border-amber rounded text-size-lg"
        >tsc --jsx {{ jsx }}
        <template v-if="factory">--jsxFactory {{ factory }}</template></span
      >
    </p>
  </div>
</template>
