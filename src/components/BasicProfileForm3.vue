<!-- // Step 3: Pattern Validation -- Project: Addind Regex to input fields -->

<script setup>
import { ref, reactive } from 'vue';

const successMessage = ref('');

const form = reactive({
    name: '',
    email: '',
    age: '',
    phone: ''
});

const resetForm = () => {
    form.name = '';
    form.email = '';
    form.age = '';
    form.phone = '';
};

// Create errors for the form

const errors = reactive({
    name: '',
    email: '',
    age: '',
    phone: ''
});

const resetErrors = () => {
    errors.name = '';
    errors.email = '';
    errors.age = '';
    errors.phone = '';
};

// The Validation Function
const validateForm = () => {
    const nameRegex = /^[a-zA-Z\s]{2,}$/;
    const emailRegex = /^\S+@\S+\.\S+$/;
    const passwordRegex = /^(?=.*[A-Za-z])(?=.*\d)[A-Za-z\d]{8,}$/;
    const phoneRegex = /^\d{10}$/;

    errors.name = !form.name
        ? "Name is required"
        : !nameRegex.test(form.name)
            ? "Name must be at least 2 letters and only contain letters and spaces"
            : "";

    errors.email = !form.email
        ? "Email is required"
        : !emailRegex.test(form.email)
            ? "Enter a valid email address"
            : "";

    // errors.password = !form.password
    //     ? "Password is required"
    //     : !passwordRegex.test(form.password)
    //         ? "Password must be at least 8 characters and include a number"
    //         : "";

    errors.phone = !form.phone
        ? "Phone number is required"
        : !phoneRegex.test(form.phone)
            ? "Phone number must be 10 digits"
            : "";

    errors.age = !form.age
        ? "Age is required"
        : isNaN(Number(form.age))
            ? "Age must be a number"
            : Number(form.age) < 18
                ? "You must be at least 18 years old"
                : "";

    // errors.terms = !form.terms ? "You must agree to the terms" : "";

    return !Object.values(errors).some((error) => error);
};

// The Submit Form Function
const submitForm = () => {
    const isValid = validateForm();

    if (!isValid) {
        successMessage.value = ''; // Clear message if there are errors
        return;
    }

    // If valid, show message
    successMessage.value = 'Form submitted successfully!';

    // Reset form fields

    resetForm();
    //   form.name = '';
    //   form.email = '';
    //   form.age = '';
    //   form.phone = '';

    // Clear any errors

    resetErrors();
    //   errors.name = '';
    //   errors.email = '';
    //   errors.age = '';
    //   errors.phone = '';
};





</script>

<template>
    <div class="max-w-md mx-auto mt-10 p-6 bg-white shadow rounded">
        <h2 class="text-xl font-bold mb-4">Profile Form</h2>


        <form @submit.prevent="submitForm" class="space-y-4">

            <p v-if="successMessage" class="mt-4 text-green-600 text-sm">
                {{ successMessage }}
            </p>
            <div>
                <label class="block text-sm font-medium mb-1">Name</label>
                <input v-model="form.name" type="text" class="border p-2 w-full rounded" placeholder="John Doe"
                    :class="{ 'border-red-500': errors.name }" />
                <p v-if="errors.name" class="text-red-600 text-sm mt-1">{{ errors.name }}</p>
            </div>

            <div>
                <label class="block text-sm font-medium mb-1">Email</label>
                <input v-model="form.email" type="email" class="border p-2 w-full rounded"
                    placeholder="john@example.com" :class="{ 'border-red-500': errors.email }" />
                <p v-if="errors.email" class="text-red-600 text-sm mt-1">{{ errors.email }}</p>
            </div>

            <div>
                <label class="block text-sm font-medium mb-1">Age</label>
                <input v-model="form.age" type="number" class="border p-2 w-full rounded" placeholder="30"
                    :class="{ 'border-red-500': errors.age }" />
                <p v-if="errors.age" class="text-red-600 text-sm mt-1">{{ errors.age }}</p>
            </div>

            <div>
                <label class="block text-sm font-medium mb-1">Phone Number</label>
                <input v-model="form.phone" type="tel" class="border p-2 w-full rounded" placeholder="123-456-7890"
                    :class="{ 'border-red-500': errors.phone }" />
                <p v-if="errors.phone" class="text-red-600 text-sm mt-1">{{ errors.phone }}</p>
            </div>

            <button type="submit" class="bg-blue-600 text-white px-4 py-2 rounded hover:bg-blue-700">
                Submit
            </button>
        </form>

        <div class="mt-6 bg-gray-100 p-4 rounded">
            <h3 class="text-sm font-bold mb-2">Live Form Data:</h3>
            <pre>{{ form }}</pre>
        </div>
    </div>
</template>

<style scoped></style>
