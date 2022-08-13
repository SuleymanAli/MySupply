<template>
  <div class="message flex px-10 my-10" :class="{ 'ml-auto': !props.isBot }">
    <span
      class="message__icon flex text-xl self-start"
      :class="{
        'message__icon--robot': props.isBot,
        'message__icon--user order-2': !props.isBot,
      }"
    >
      <component :is="isBot ? IconRobot : null" class="m-auto" />
    </span>
    <p
      class="message__content rounded-md border-2 p-3 ml-7"
      :class="{
        'message__content--robot order-2': props.isBot,
        'message__content--user mr-7': !props.isBot,
      }"
    >
      {{ props.message }}
    </p>
  </div>
</template>

<script lang="ts" setup>
import IconRobot from './Icons/IconRobot.vue'

const props = defineProps({
  isBot: {
    type: Boolean,
    default: true,
  },
  message: {
    type: String,
    required: true,
  },
})
</script>

<style lang="scss" scoped>
.message {
  &__icon {
    width: 80px;
    height: 60px;
    border-radius: 50%;
    background: rgb(31, 128, 184);

    &--robot {
      background: orange;

      :deep() svg * {
        fill: white !important;
      }
    }
  }

  &__content {
    position: relative;

    &::before {
      content: '';
      position: absolute;
      top: 10px;
      width: 0;
      height: 0;
      border-top: 15px solid transparent;
      border-bottom: 15px solid transparent;
    }

    &--user {
      background: rgb(60, 143, 191);
      color: white;
      border-color: rgb(60, 143, 191);

      &::before {
        right: -25px;
        border-left: 25px solid rgb(60, 143, 191);
      }
    }

    &--robot {
      border: 2px solid orange;

      &::before {
        left: -25px;
        border-right: 25px solid orange;
      }
    }
  }
}
</style>
