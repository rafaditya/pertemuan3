<template>
    <p>Todo id: {{ todoId }}</p> <!-- Menampilkan id dari todo yang sedang diproses -->
    <button @click="todoId++" :disabled="!todoData">Fetch next todo</button> <!-- Tombol untuk mengambil todo berikutnya, dinonaktifkan saat data tidak tersedia -->
    <p v-if="!todoData">Loading...</p> <!-- Menampilkan pesan "Loading..." jika todoData kosong -->
    <pre v-else>{{ todoData }}</pre> <!-- Menampilkan data todo jika sudah tersedia -->
  </template>
  
  <script setup>
  import { ref, watch } from 'vue' //<!-- Mengimpor ref untuk variabel reaktif dan watch untuk reaksi terhadap perubahan -->
  
  const todoId = ref(1) //<!-- Membuat variabel reaktif untuk menyimpan id todo, dimulai dari 1 -->
  const todoData = ref(null) //<!-- Membuat variabel reaktif untuk menyimpan data todo, awalnya kosong -->
  
  async function fetchData() { //<!-- Fungsi untuk mengambil data todo dari API secara asinkron -->
    todoData.value = null //<!-- Menyetel todoData menjadi null saat sedang mengambil data -->
    const res = await fetch( //<!-- Melakukan fetch ke API untuk mendapatkan todo berdasarkan todoId -->
      `https://jsonplaceholder.typicode.com/todos/${todoId.value}` //<!-- Menggunakan todoId untuk menentukan todo yang diambil -->
    )
    todoData.value = await res.json() //<!-- Menyimpan hasil JSON ke dalam todoData -->
  }
  
  fetchData() //<!-- Memanggil fetchData untuk mengambil data todo pertama kali -->
  
  watch(todoId, fetchData) //<!-- Mengawasi perubahan pada todoId dan memanggil fetchData jika todoId berubah -->
  </script>
  