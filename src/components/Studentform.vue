<script setup>
import { defineProps, defineEmits } from 'vue'

const props = defineProps({
  npm: String,
  nama: String,
  kelas: String
})

const emit = defineEmits(['update:npm', 'update:nama', 'update:kelas', 'create', 'update', 'del'])

function updateNpm(event) {
  emit('update:npm', event.target.value)
}

function updateNama(event) {
  emit('update:nama', event.target.value)
}

function updateKelas(event) {
  emit('update:kelas', event.target.value)
}

function create() {
  emit('create')
}

function update() {
  emit('update')
}

function del() {
  emit('del')
}
</script>

<template>
  <div>
    <div class="form-container">
      <label>NPM: <input :value="npm" @input="updateNpm"></label>
    </div>

    <div class="form-container">
      <label>Nama: <input :value="nama" @input="updateNama"></label>
    </div>

    <div class="form-container">
      <label>Kelas: <input :value="kelas" @input="updateKelas"></label>
    </div>

    <div class="buttons">
      <button @click="create">Create</button>
      <button @click="update">Update</button>
      <button @click="del">Delete</button>
    </div>
  </div>
</template>

<style>
.form-container {
  margin-bottom: 20px;
}

.buttons {
  display: flex;
}

.buttons button + button {
  margin-left: 10px;
}
</style>
