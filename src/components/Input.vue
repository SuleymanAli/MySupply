<template>
  <div class="input flex py-7 pl-7 pr-10 border-2 border-sky-200 rounded-md">
    <div class="input__main grow relative mr-4">
      <input
        v-model="inputValue"
        type="text"
        class="border-2 border-gray-400 rounded-md p-3 pr-10 w-full"
      />
      <span class="absolute top-1/2 right-4 -translate-y-1/2 text-lg">
        <IconEuro />
      </span>
    </div>
    <button
      @click.prevent="handleSubmit"
      class="input__cta bg-cyan-800 px-6 py-3 rounded-md text-white"
    >
      SEND
    </button>
  </div>
</template>

<script setup>
import IconEuro from './Icons/IconEuro.vue'
import { ref, toRefs, watch } from 'vue'
const emit = defineEmits(['send:price'])
const props = defineProps(['progressBarStatus'])
const progressBarStatus = toRefs(props).progressBarStatus

const inputValue = ref('')

function handleSubmit() {
  emit('send:price', inputValue.value)
}

watch(progressBarStatus, () => {
  if (!inputValue.value) emit('send:price', false)
})
</script>

<style lang="scss" scoped>
.input {
  &__main {
  }
  &__cta {
  }
}
</style>
