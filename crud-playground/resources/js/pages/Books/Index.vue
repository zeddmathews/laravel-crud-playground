<script setup lang="ts">
import AppLayout from '@/layouts/AppLayout.vue';
import { Head, Link, router } from '@inertiajs/vue3';
import type { Book } from '@/types/book';
import { ref } from 'vue';

defineOptions({ layout: AppLayout });

interface Props {
  books: Book[];
  search?: string;
}

const { books, search } = defineProps<Props>();

const searchQuery = ref(search ?? '');

const submitSearch = () => {
  router.get(route('books.index'), { search: searchQuery.value }, {
    preserveState: true,
    preserveScroll: true,
  });
};

const deleteBook = (id: number) => {
  if (confirm('Are you sure you want to delete this book?')) {
    router.delete(route('books.destroy', id));
  }
};
</script>

<template>
  <Head title="Books" />

  <div class="flex flex-col gap-4 mb-6 sm:flex-row sm:items-center sm:justify-between">
    <h1 class="text-2xl font-semibold text-gray-900 dark:text-gray-100">Bookshelf</h1>

    <div class="flex flex-col sm:flex-row gap-2 items-stretch">
      <input
        v-model="searchQuery"
        type="text"
        placeholder="Search by title..."
        class="px-3 py-2 rounded border dark:border-gray-700 dark:bg-gray-900 dark:text-gray-100 focus:outline-none focus:ring-2 focus:ring-blue-600"
        @keyup.enter="submitSearch"
      />
      <button
        @click="submitSearch"
        class="bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded transition"
      >
        🔍 Search
      </button>
      <Link
        :href="route('books.create')"
        class="bg-green-600 hover:bg-green-700 text-white px-4 py-2 rounded transition"
      >
        ➕ Add New Book
      </Link>
    </div>
  </div>

  <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
    <div
      v-for="book in books"
      :key="book.id"
      class="bg-white dark:bg-gray-800 border border-gray-200 dark:border-gray-700 p-5 rounded-lg shadow-sm hover:shadow-lg transition"
    >
      <h2 class="text-lg font-bold text-gray-900 dark:text-gray-100">{{ book.title }}</h2>
      <p class="text-sm text-gray-600 dark:text-gray-400">{{ book.author }}</p>
      <p class="mt-2 text-gray-700 dark:text-gray-300">{{ book.description }}</p>
      <p class="mt-2 text-sm italic text-gray-500 dark:text-gray-400">Genre: {{ book.genre }}</p>

      <div class="mt-4 flex gap-3">
        <Link
          :href="route('books.edit', book.id)"
          class="inline-flex items-center px-3 py-1.5 text-sm font-medium bg-indigo-600 hover:bg-indigo-700 text-white rounded-md transition"
        >
          ✏️ Edit
        </Link>

        <button
          @click="deleteBook(book.id)"
          class="inline-flex items-center px-3 py-1.5 text-sm font-medium bg-red-600 hover:bg-red-700 text-white rounded-md transition"
        >
          🗑️ Delete
        </button>
      </div>
    </div>
  </div>
</template>
