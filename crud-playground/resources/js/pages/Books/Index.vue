<script setup lang="ts">
import AppLayout from '@/layouts/AppLayout.vue';
import { Head, Link } from '@inertiajs/vue3';
import type { Book } from '@/types/book';

defineOptions({ layout: AppLayout });

interface Props {
  books: Book[];
}

const { books } = defineProps<Props>();
</script>

<template>
  <Head title="Books" />

  <div class="flex items-center justify-between mb-6">
    <h1 class="text-2xl font-semibold">Bookshelf</h1>
    <Link
      :href="route('books.create')"
      class="bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded"
    >
      ➕ Add New Book
    </Link>
  </div>

  <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
    <div
      v-for="book in books"
      :key="book.id"
      class="bg-white p-4 rounded shadow hover:shadow-md transition"
    >
      <h2 class="text-lg font-bold">{{ book.title }}</h2>
      <p class="text-sm text-gray-500">{{ book.author }}</p>
      <p class="mt-2">{{ book.description }}</p>
      <div class="mt-4 text-sm text-gray-600 italic">Genre: {{ book.genre }}</div>
    </div>
  </div>
</template>
