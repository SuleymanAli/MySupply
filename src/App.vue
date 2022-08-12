<template>
  <div>
    <!-- Message History -->
    <div>
      <Messages />
    </div>
    <!-- Input -->
    <div class="">
      <ProgressBar />
      <Input />
    </div>
  </div>
</template>

<script lang="ts" setup>
import Input from './components/Input.vue'
import Messages from './components/Messages.vue'
import ProgressBar from './components/ProgressBar.vue'
</script>

<style lang="scss" scoped></style>
