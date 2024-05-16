<script setup>
import { defineProps, defineEmits } from 'vue'

const props = defineProps({
  students: Array,
  selected: String
})

const emit = defineEmits(['update:selected'])

function updateSelected(event) {
  emit('update:selected', event.target.value)
}
</script>

<template>
  <div class="selection-container">
    <select size="5" :value="selected" @change="updateSelected">
      <option v-for="name in students" :key="name">{{ name }}</option>
    </select>
  </div>
</template>

<style>
.selection-container {
  margin-bottom: 20px;
}
</style>
