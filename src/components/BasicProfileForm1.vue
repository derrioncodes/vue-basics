<!-- // Step 1: Understanding v-model -- Project: Basic Profile Form - Binding inputs -->

<script setup>
import { reactive } from 'vue';

const form = reactive({
    name: '',
    email: '',
    age: '',
    phone: ''
});

const resetForm = reactive({
    name: '',
    email: '',
    age: '',
    phone: ''
});
</script>

<template>
    <div class="max-w-md mx-auto mt-10 p-6 bg-white shadow rounded">
        <h2 class="text-xl font-bold mb-4">Profile Form</h2>

        <form class="space-y-4">
            <div>
                <label class="block text-sm font-medium mb-1">Name</label>
                <input v-model="form.name" type="text" class="border p-2 w-full rounded" placeholder="John Doe" />
            </div>

            <div>
                <label class="block text-sm font-medium mb-1">Email</label>
                <input v-model="form.email" type="email" class="border p-2 w-full rounded"
                    placeholder="john@example.com" />
            </div>

            <div>
                <label class="block text-sm font-medium mb-1">Age</label>
                <input v-model="form.age" type="number" class="border p-2 w-full rounded" placeholder="30" />
            </div>

            <div v-if="form.name">
                <label class="block text-sm font-medium mb-1">Phone Number</label>
                <input v-model="form.phone" type="tel" class="border p-2 w-full rounded" placeholder="123-456-7890" />
            </div>

            <button @click="resetForm"
                class="w-full flex justify-center py-2 px-4 border border-transparent rounded-lg shadow-sm text-sm font-medium text-white bg-primary-600 hover:bg-primary-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-primary-500 transition-colors">

                Reset

            </button>
        </form>

        <div class="mt-6 bg-gray-100 p-4 rounded">
            <h3 class="text-sm font-bold mb-2">Live Form Data:</h3>
            <pre>{{ form }}</pre>
        </div>
    </div>
</template>

<style scoped></style>
