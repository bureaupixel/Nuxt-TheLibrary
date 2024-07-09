<template>
    <div>
      <p class="text-3xl font-bold mb-10">All Books:</p>
      <ul>
        <li v-for="book in books" :key="book.id">
            <div class="text-xl font-bold">
                <RouterLink :to="`/books/${book.id}`">
                    {{ book.title }}
                </RouterLink>
            </div>
            <hr>
        </li>
      </ul>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  const books = ref([]);
  onMounted(async () => {
    try {
      const response = await fetch('/data/books.json');
      const data = await response.json();
      books.value = data.map(book => ({
        id: book.id,
        title: book.title
      }));
    } catch (error) {
      console.error('Error fetching data:', error);
    }
  });
  </script>
  