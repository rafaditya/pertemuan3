<template>
  <div class="todo-app"> <!-- Container utama untuk aplikasi todo -->
    <form @submit.prevent="addTodo" class="todo-form">  <!-- Form untuk menambahkan todo baru -->
      <input v-model="newTodo" required placeholder="new todo" class="todo-input"> <!-- Input teks untuk todo baru -->
      <button type="submit" class="todo-button">Add Todo</button> <!-- Tombol untuk menambahkan todo -->
    </form>

    <ul class="todo-list"> <!-- Daftar todo -->
      <li v-for="todo in filteredTodos" :key="todo.id" class="todo-item"> <!-- Loop untuk menampilkan todo -->
        <input type="checkbox" v-model="todo.done"> <!-- Kotak centang untuk menandai todo selesai -->
        <span :class="{ done: todo.done }">{{ todo.text }}</span> <!-- Teks todo, garis bawah jika selesai -->
        <button @click="removeTodo(todo)" class="delete-button">X</button> <!-- Tombol untuk menghapus todo -->
      </li>
    </ul>

    <button @click="hideCompleted = !hideCompleted" class="toggle-completed"> <!-- Tombol untuk menyembunyikan/menampilkan todo yang selesai -->
      {{ hideCompleted ? 'Show all' : 'Hide completed' }} <!-- Teks tombol sesuai status -->
    </button>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue' // Import ref dan computed dari Vue

let id = 0 // Variabel id untuk menghasilkan ID unik untuk setiap todo

const newTodo = ref('') // Reactive variable untuk menyimpan teks todo baru
const hideCompleted = ref(false) // Reactive variable untuk status sembunyikan todo yang selesai
const todos = ref([ // Daftar todo awal
  { id: id++, text: 'Learn HTML', done: true },
  { id: id++, text: 'Learn JavaScript', done: true },
  { id: id++, text: 'Learn Vue', done: false }
])

const filteredTodos = computed(() => { // Menghitung daftar todo berdasarkan hideCompleted
  return hideCompleted.value
    ? todos.value.filter((t) => !t.done) // Jika hideCompleted true, sembunyikan todo yang selesai
    : todos.value // Jika false, tampilkan semua todo
})

function addTodo() { // Fungsi untuk menambahkan todo baru
  todos.value.push({ id: id++, text: newTodo.value, done: false }) // Tambahkan todo baru ke daftar
  newTodo.value = '' // Kosongkan input setelah menambahkan todo
}

function removeTodo(todo) { // Fungsi untuk menghapus todo
  todos.value = todos.value.filter((t) => t.id !== todo.id) // Hapus todo berdasarkan id
}
</script>
<style>

.done {  
  text-decoration: line-through;
}
</style>

