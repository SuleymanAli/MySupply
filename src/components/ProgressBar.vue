<template>
  <Transition>
    <div v-if="isRunning">
      <div><div class="progressBar bg-sky-400"></div></div>
      {{ time }} seconds
    </div>
  </Transition>
</template>

<script lang="ts" setup>
import { onMounted, ref } from 'vue'

const emit = defineEmits(['toggle:ProgressBar'])
const props = defineProps(['progressbar'])

let time = ref(3)
const isRunning = ref(true)

onMounted(() => {
  setInterval(incrementTime, 1000)
})

function incrementTime() {
  time.value = time.value - 1
  if (time.value === 0) {
    emit('toggle:ProgressBar', false)
    isRunning.value = false
  }
}
</script>

<style lang="scss" scoped>
.progressBar {
  width: 100px;
  height: 5px;
  border-radius: 5px;
  animation: decreasing 15s infinite;

  @keyframes decreasing {
    from {
      width: 300px;
    }
    to {
      width: 0;
    }
  }
}
</style>
