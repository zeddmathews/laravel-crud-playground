<script setup lang="ts">
import AppLayout from '@/layouts/AppLayout.vue';
import { useForm, Head, Link } from '@inertiajs/vue3';
import InputError from '@/components/InputError.vue';
import { Label } from '@/components/ui/label';
import { Input } from '@/components/ui/input';
import Textarea from '@/components/ui/TextArea.vue';
import { Button } from '@/components/ui/button';
import { LoaderCircle } from 'lucide-vue-next';
import type { Book } from '@/types/book';

defineOptions({ layout: AppLayout });

interface Props {
  book: Book;
}

const { book } = defineProps<Props>();

const form = useForm({
  title: book.title,
  author: book.author,
  genre: book.genre,
  description: book.description,
});

const submit = () => {
  form.put(route('books.update', book.id));
};
</script>

<template>
  <Head title="Edit Book" />

  <div class="max-w-xl mx-auto p-6 bg-white dark:bg-gray-900 rounded-lg shadow-md">
    <div class="flex justify-between items-center mb-6">
      <h1 class="text-2xl font-semibold text-gray-900 dark:text-gray-100">Edit Book</h1>
      <Link :href="route('books.index')" class="text-sm text-blue-600 dark:text-blue-400 hover:underline">
        ← Back to list
      </Link>
    </div>

    <form @submit.prevent="submit" class="flex flex-col gap-6">
      <div class="grid gap-4">
        <div class="grid gap-2">
          <Label for="title" class="text-gray-700 dark:text-gray-300">Title</Label>
          <Input id="title" v-model="form.title" required autocomplete="off" />
          <InputError :message="form.errors.title" />
        </div>

        <div class="grid gap-2">
          <Label for="author" class="text-gray-700 dark:text-gray-300">Author</Label>
          <Input id="author" v-model="form.author" required />
          <InputError :message="form.errors.author" />
        </div>

        <div class="grid gap-2">
          <Label for="genre" class="text-gray-700 dark:text-gray-300">Genre</Label>
          <Input id="genre" v-model="form.genre" required />
          <InputError :message="form.errors.genre" />
        </div>

        <div class="grid gap-2">
          <Label for="description" class="text-gray-700 dark:text-gray-300">Description</Label>
          <Textarea id="description" v-model="form.description" :rows="4" required />
          <InputError :message="form.errors.description" />
        </div>
      </div>

      <Button type="submit" class="mt-4 w-full" :disabled="form.processing">
        <LoaderCircle v-if="form.processing" class="h-4 w-4 animate-spin mr-2" />
        Update Book
      </Button>
    </form>
  </div>
</template>
