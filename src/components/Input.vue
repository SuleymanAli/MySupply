<template>
  <div class="input flex py-7 pl-7 pr-10 border-2 border-sky-200 rounded-md">
    <div class="input__main grow relative mr-4">
      <input
        type="text"
        class="border-2 border-gray-400 rounded-md p-3 pr-10 w-full"
      />
      <span class="absolute top-1/2 right-4 -translate-y-1/2 text-lg">
        <IconEuro />
      </span>
    </div>
    <button class="input__cta bg-cyan-800 px-6 py-3 rounded-md text-white">
      SEND
    </button>
  </div>
</template>

<script lang="ts" setup>
import IconEuro from './Icons/IconEuro.vue'
</script>

<style lang="scss" scoped>
.input {
  &__main {
  }
  &__cta {
  }
}
</style>
