<template>
  <div>
    <h1 class="text-2xl font-bold mb-4">Book List</h1>

    <table class="min-w-full border border-gray-300">
      <thead class="bg-gray-100">
        <tr>
          <th class="p-2 text-left">Title</th>
          <th class="p-2 text-left">Author</th>
          <th class="p-2 text-left">Genre</th>
          <th class="p-2 text-left">Description</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="book in books" :key="book.id" class="border-t">
          <td class="p-2">{{ book.title }}</td>
          <td class="p-2">{{ book.author }}</td>
          <td class="p-2">{{ book.genre }}</td>
          <td class="p-2">{{ book.description }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup lang="ts">
interface Book {
  id: number;
  title: string;
  author: string;
  genre: string;
  description: string;
}

defineProps<{
  books: Book[];
}>();
</script>
