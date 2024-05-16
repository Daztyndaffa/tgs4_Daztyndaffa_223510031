<script setup>
import { defineProps, defineEmits } from 'vue'

const props = defineProps({
  prefix: String
})

const emit = defineEmits(['update:prefix'])

function updatePrefix(event) {
  emit('update:prefix', event.target.value)
}
</script>

<template>
  <div class="filter-container">
    <input :value="prefix" @input="updatePrefix" placeholder="Filter prefix" />
  </div>
</template>

<style>
.filter-container {
  margin-bottom: 20px;
}
</style>
