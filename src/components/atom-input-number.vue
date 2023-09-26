<template>
  <div class="atom-input-number-wrapper">
    <label for="session" class="atom-input-number-label"> {{ label }} </label>
    <input
      type="number"
      name="session"
      min="1"
      max="59"
      :value="value"
      :disabled="disabled"
      @input="$emit('updateTime', $event.target.value)"
      class="atom-input-number"
    />
  </div>
</template>

<script setup>
defineProps({
  label: String,
  value: Number,
  disabled: Boolean
})
</script>

<style scoped>
.atom-input-number-wrapper {
  width: 100%;
}

.atom-input-number {
  width: 100%;
}

.atom-input-number-label {
  font-size: 1rem;
}
</style>
