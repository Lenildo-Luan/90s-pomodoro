<script setup>
import Pomodoro from './components/pomodoro-app.vue'
</script>

<template>
  <main>
    <section class="section-pomodoro">
      <Pomodoro/>
    </section>
  </main>
</template>

<style scoped>
.section-pomodoro {
  height: 100vh;

  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
