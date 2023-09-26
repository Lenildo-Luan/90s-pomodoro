<template>
  <div class="pomodoro-app">
    <div class="pomodoro-input-wrapper">
      <Input
        label="Session length (min):"
        :value="sessionLength"
        @update-time="updateSessionTime"
        :disabled="isInputDisabled"
      />
      <Input
        label="Break length (min):"
        :value="breakLength"
        @update-time="updateBreakTime"
        :disabled="isInputDisabled"
      />
    </div>

    <Countdown :minutes="currentMinutes" :seconds="currentSeconds" />

    <Button v-if="!isRunning" :content="startButtonContent" @action="startCountdown" />
    <Button v-else content="Reset" @action="stopCountdown" />
  </div>
</template>

<script setup>
//Imports
import { ref, computed } from 'vue'
import Input from './atom-input-number.vue'
import Countdown from './atom-countdown.vue'
import Button from './atom-button.vue'

// Properties
const setIntervalId = ref(null)

const sessionLength = ref(25)
const breakLength = ref(5)

const currentMinutes = ref(sessionLength.value)
const currentSeconds = ref(0)

const isSession = ref(true)
const isRunning = ref(false)
const isInputDisabled = ref(false)

// Methods
function updateSessionTime(time) {
  sessionLength.value = parseInt(time)
  if (isSession.value) currentMinutes.value = parseInt(time)
}

function updateBreakTime(time) {
  breakLength.value = parseInt(time)
  if (!isSession.value) currentMinutes.value = parseInt(time)
}

function startCountdown() {
  isRunning.value = true
  isInputDisabled.value = true

  setIntervalId.value = setInterval(updateCountdown, 1000)
}

function updateCountdown() {
  if (currentMinutes.value + currentSeconds.value === 0) {
    clearInterval(setIntervalId.value)
    updateCountdownMode()
    
    isRunning.value = false
    isInputDisabled.value = false
  } else if (currentSeconds.value === 0) {
    currentMinutes.value -= 1
    currentSeconds.value = 59
  } else {
    currentSeconds.value -= 1
  }
}

function stopCountdown() {
  isRunning.value = false
  isInputDisabled.value = false

  clearInterval(setIntervalId.value)

  currentMinutes.value = sessionLength.value
  currentSeconds.value = 0
}

function updateCountdownMode() {
    if (isSession.value) {
      isSession.value = false
      currentMinutes.value = breakLength.value
    } else {
      isSession.value = true
      currentMinutes.value = sessionLength.value
    }
}

// Computed
const startButtonContent = computed(() => (isSession.value ? 'Start work' : 'Start break'))
</script>

<style scoped>
.pomodoro-app {
  width: 100%;
  max-width: 480px;
}

.pomodoro-input-wrapper {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  column-gap: 1rem;

  margin-bottom: 2rem;
}
</style>
