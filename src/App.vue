<template>
  <div class="homePage">
    <!-- Message History -->
    <div class="homePage__messageList flex flex-col mb-10">
      <Messages
        v-for="(data, index) in datas"
        :key="index"
        :message="data.message"
        :isBot="data.bot"
      />
    </div>
    <div class="flex flex-col items-center">
      <!-- Progress Bar -->
      <ProgressBar
        class="w-1/4 grow mb-7"
        @toggle:ProgressBar="handleProgressBar"
        :progressbar="progressBarStatus"
      />
      <!-- Input -->
      <Input
        class="w-1/2"
        :class="{ hidden: progressBarStatus }"
        :progressBarStatus="progressBarStatus"
        @send:price="handlePrice"
      />
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref, watch } from 'vue'
import Input from './components/Input.vue'
import Messages from './components/Messages.vue'
import ProgressBar from './components/ProgressBar.vue'

/* Progress Bar */
const progressBarStatus = ref(false)
function handleProgressBar(value) {
  progressBarStatus.value = !progressBarStatus.value
}

/* Messages */
const datas = ref([
  {
    message: 'Hello',
    bot: true,
    requirePrice: false,
  },

  {
    message: 'Hi',
    bot: false,
    requirePrice: false,
  },

  {
    message:
      'the current price of € 10 000 is too high and requesting a lower one',
    bot: true,
    requirePrice: true,
  },
])

onMounted(() => {
  checkLastMessage()
})

watch(datas.value, () => {
  checkLastMessage()
})

const checkLastMessage = () =>
  datas.value.findLast((c) => c?.requirePrice === true)

/*  */
const handlePrice = (value) => {
  if (value) {
    datas.value.push({
      message: value,
      bot: false,
    })
  } else {
    datas.value.push({
      message: 'Please hurry',
      bot: true,
      requirePrice: true,
    })
  }
  return value
}
</script>

<style lang="scss" scoped>
.homePage {
  display: flex;
  flex-direction: column;

  &__messageList {
    box-shadow: inset 0px -10px 10px 1px lightgrey;
    max-height: 80vh;
    overflow-y: auto;
  }
}
</style>
