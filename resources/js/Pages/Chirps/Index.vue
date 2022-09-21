<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import Chirp from '@/Components/Chirp.vue';
import InputError from '@/Components/InputError.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import { useForm, Head } from '@inertiajs/inertia-vue3';

defineProps(['chirps']);

const form = useForm({
    message: '',
    color: '',
});
</script>

<template>

  <Head title="Chirps" />

  <AuthenticatedLayout>
      <div class="max-w-2xl mx-auto p-4 mt-4 sm:p-6 lg:p-8" style="max-width: 42rem;">
        <form @submit.prevent="form.post(route('chirps.store'), { onSuccess: () => form.reset() })" class="flex flex-col">
          <textarea v-model="form.message" placeholder="What's on your mind right now?"
            class="block w-full border-gray-300 focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm"></textarea>
          <InputError :message="form.errors.message" class="mt-2" />
          <input type="text" v-model="form.color" placeholder="border color" class="mt-4 border-gray-300 focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm"/>
          <PrimaryButton class="mt-4 w-24 text-center flex items-center justify-center">Chirp</PrimaryButton>
        </form>

        <div class="mt-6 space-y-4">
          <Chirp v-for="chirp in chirps" :key="chirp.id" :chirp="chirp" />
        </div>
      </div>
  </AuthenticatedLayout>
</template>
