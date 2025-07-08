<script setup lang="ts">
import AppLayout from '@/layouts/AppLayout.vue';
import { useForm, Head, Link } from '@inertiajs/vue3';
import InputError from '@/components/InputError.vue';
import { Label } from '@/components/ui/label';
import { Input } from '@/components/ui/input';
import Textarea from '@/components/ui/TextArea.vue';
import { Button } from '@/components/ui/button';
import { LoaderCircle } from 'lucide-vue-next';

defineOptions({ layout: AppLayout });

const form = useForm({
  title: '',
  author: '',
  genre: '',
  description: '',
});

const submit = () => {
  form.post(route('books.store'), {
    onFinish: () => form.reset(),
  });
};
</script>

<template>
  <Head title="Add Book" />

  <div class="max-w-xl mx-auto p-6 bg-white rounded shadow">
    <div class="flex justify-between items-center mb-4">
      <h1 class="text-xl font-semibold">Add a New Book</h1>
      <Link :href="route('books.index')" class="text-blue-600 hover:underline text-sm">
        ← Back to list
      </Link>
    </div>

    <form @submit.prevent="submit" class="space-y-4">
      <div>
        <Label for="title">Title</Label>
        <Input id="title" v-model="form.title" required autocomplete="off" />
        <InputError :message="form.errors.title" />
      </div>

      <div>
        <Label for="author">Author</Label>
        <Input id="author" v-model="form.author" required />
        <InputError :message="form.errors.author" />
      </div>

      <div>
        <Label for="genre">Genre</Label>
        <Input id="genre" v-model="form.genre" required />
        <InputError :message="form.errors.genre" />
      </div>

      <div>
        <Label for="description">Description</Label>
        <Textarea id="description" v-model="form.description" :rows="4" required />
        <InputError :message="form.errors.description" />
      </div>

      <Button type="submit" class="w-full" :disabled="form.processing">
        <LoaderCircle v-if="form.processing" class="animate-spin mr-2 h-4 w-4" />
        Save Book
      </Button>
    </form>
  </div>
</template>
