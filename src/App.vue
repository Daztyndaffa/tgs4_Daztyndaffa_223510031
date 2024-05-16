<script setup>
import { ref, reactive, computed, watch } from 'vue'
import FilterInput from './components/Filterinput.vue'
import StudentList from './components/Studentlist.vue'
import StudentForm from './components/Studentform.vue'
import SlotCom from './components/Slot.vue'

const students = reactive(['223510001, Daztyn, B', '223510002, Daffa, A', '223510003, Danendra, C'])
const selected = ref('')
const prefix = ref('')
const npm = ref('')
const nama = ref('')
const kelas = ref('')
const message = ref('')

const filteredNames = computed(() =>
  students.filter((n) =>
    n.toLowerCase().startsWith(prefix.value.toLowerCase())
  )
)

watch(selected, (name) => {
  ;[npm.value, nama.value, kelas.value] = name.split(', ')
})

function create() {
  if (hasValidInput()) {
    const Student = `${npm.value}, ${nama.value}, ${kelas.value}`
    if (!students.includes(Student)) {
      students.push(Student)
      npm.value = nama.value = kelas.value = ''
      message.value = 'Data berhasil dibuat.'
    } else {
      message.value = 'Data sudah ada.'
    }
  } else {
    message.value = 'Input tidak valid.'
  }
}

function update() {
  if (hasValidInput() && selected.value) {
    const i = students.indexOf(selected.value)
    students[i] = selected.value = `${npm.value}, ${nama.value}, ${kelas.value}`
    message.value = 'Data berhasil diperbarui.'
  } else {
    message.value = 'Input tidak valid atau tidak ada data yang dipilih.'
  }
}

function del() {
  if (selected.value) {
    const i = students.indexOf(selected.value)
    students.splice(i, 1)
    selected.value = npm.value = nama.value = kelas.value = ''
    message.value = 'Data berhasil dihapus.'
  } else {
    message.value = 'Tidak ada data yang dipilih.'
  }
}

function hasValidInput() {
  return npm.value.trim() && nama.value.trim() && kelas.value.trim()
}
</script>

<template>
  <div class="container">
    <header>
      <div class="logo-container">
        <a href="https://vitejs.dev" target="_blank">
          <img src="/vite.svg" class="logo" alt="Vite logo" />
        </a>
        <a href="https://vuejs.org/" target="_blank">
          <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
        </a>
      </div>
      
      <SlotCom />
    </header>

    <FilterInput v-model:prefix="prefix" />

    <StudentList
      :students="filteredNames"
      v-model:selected="selected"
    />

    <StudentForm
      v-model:npm="npm"
      v-model:nama="nama"
      v-model:kelas="kelas"
      @create="create"
      @update="update"
      @del="del"
    />

    <div v-if="message" class="message">
      {{ message }}
    </div>
  
  </div>
</template>


<style>
.container {
  max-width: 600px;
  margin: 0 auto;
}

.logo-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.filter-container {
  margin-bottom: 20px;
}

.selection-container {
  margin-bottom: 20px;
}

.form-container {
  margin-bottom: 20px;
}

.buttons {
  display: flex;
}

.buttons button + button {
  margin-left: 10px;
}

.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}

.done {
  text-decoration: line-through;
}

.message {
  margin-top: 20px;
  padding: 10px;
  background-color: #e0ffe0;
  border: 1px solid #b0ffb0;
  color: #007f00;
  border-radius: 5px;
}
</style>
