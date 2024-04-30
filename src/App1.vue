<template>
    <button @click="increment">Tambah</button> <!-- Tombol yang, saat diklik, akan menambah nilai count -->
    <p>Jumlah: {{ count }}</p> <!-- Menampilkan nilai count dalam template -->
  </template>
  
  <script setup>
  import { ref, onUpdated } from 'vue' //<!-- Mengimpor ref untuk reaktivitas dan onUpdated untuk lifecycle hook -->
  
  const count = ref(0) //<!-- Membuat variabel reaktif bernama count dengan nilai awal 0 -->
  
  onUpdated(() => { //<!-- Lifecycle hook yang dieksekusi setiap kali komponen diperbarui -->
    console.log("Komponen diperbarui") //<!-- Pesan konsol yang menunjukkan bahwa komponen telah diperbarui -->
  })
  
  function increment() {//{ <!-- Fungsi yang menambah nilai count setiap kali dipanggil -->
    count.value += 1 //<!-- Menambah nilai count sebanyak 1 -->
  }
  </script>
  