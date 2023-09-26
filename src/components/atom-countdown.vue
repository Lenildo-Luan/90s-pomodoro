<template>
  <h1 class="atom-countdown">{{ formatedTime }}</h1>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  minutes: Number,
  seconds: Number
})

const formatedTime = computed(() => {
  const formatedMinuts = props.minutes < 10 ? `0${props.minutes}` : `${props.minutes}`
  const formatedSeconds = props.seconds < 10 ? `0${props.seconds}` : `${props.seconds}`

  return `${formatedMinuts}:${formatedSeconds}`
})
</script>

<style scoped>
.atom-countdown {
  width: 100%;
  margin-bottom: 2rem;

  font-size: 13rem;
  text-align: center;
}
</style>
