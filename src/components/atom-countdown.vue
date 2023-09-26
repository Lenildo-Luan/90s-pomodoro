<template>
  <h1 class="atom-countdown">{{ formattedTime }}</h1>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  minutes: Number,
  seconds: Number
})

const formattedTime = computed(() => {
  const {minutes, seconds} = props  

  const formattedMinutes = minutes < 10 ? `0${minutes}` : `${minutes}`
  const formattedSeconds = seconds < 10 ? `0${seconds}` : `${seconds}`

  return `${formattedMinutes}:${formattedSeconds}`
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
