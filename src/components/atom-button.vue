<template>
  <button class="atom-button" @click="$emit('action')">{{ props.content }}</button>
</template>

<script setup>
const props = defineProps({
  content: String
})
</script>

<style scoped>
.atom-button {
  width: 100%;
  padding: 1rem 0;

  font-size: 1rem;
  font-weight: bold;
  text-transform: uppercase;
}
</style>
