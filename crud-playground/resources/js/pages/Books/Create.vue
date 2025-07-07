<script setup lang="ts">
import { useForm } from '@inertiajs/vue3';

const form = useForm({
  title: '',
  author: '',
  genre: '',
  description: '',
});

const submit = () => {
  form.post(route('books.store'), {
    onFinish: () => { form.reset(); },
  });
}
</script>

<template>
  <div class="max-w-md mx-auto p-4">
    <h1 class="text-2xl font-bold mb-6">Add New Book</h1>

    <form @submit.prevent="submit" novalidate>
      <div class="mb-4">
        <label for="title" class="block font-semibold mb-1">Title</label>
        <input
          id="title"
          type="text"
          v-model="form.title"
          class="w-full border rounded px-3 py-2"
          required
        />
        <p v-if="form.errors.title" class="text-red-600 text-sm mt-1">
          {{ form.errors.title }}
        </p>
      </div>

      <div class="mb-4">
        <label for="author" class="block font-semibold mb-1">Author</label>
        <input
          id="author"
          type="text"
          v-model="form.author"
          class="w-full border rounded px-3 py-2"
          required
        />
        <p v-if="form.errors.author" class="text-red-600 text-sm mt-1">
          {{ form.errors.author }}
        </p>
      </div>

      <div class="mb-4">
        <label for="genre" class="block font-semibold mb-1">Genre</label>
        <input
          id="genre"
          type="text"
          v-model="form.genre"
          class="w-full border rounded px-3 py-2"
          required
        />
        <p v-if="form.errors.genre" class="text-red-600 text-sm mt-1">
          {{ form.errors.genre }}
        </p>
      </div>

      <div class="mb-6">
        <label for="description" class="block font-semibold mb-1">Description</label>
        <textarea
          id="description"
          v-model="form.description"
          rows="4"
          class="w-full border rounded px-3 py-2"
          required
        ></textarea>
        <p v-if="form.errors.description" class="text-red-600 text-sm mt-1">
          {{ form.errors.description }}
        </p>
      </div>

      <button
        type="submit"
        class="bg-blue-600 text-white rounded px-4 py-2 hover:bg-blue-700"
        :disabled="form.processing"
      >
        Save Book
      </button>
    </form>
  </div>
</template>
