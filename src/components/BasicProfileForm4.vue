<!-- Build each input field using v-model

Add error message display (<p v-if="errors.name">...</p>)

Use regex for name, email, and phone

Make a textarea input for "Why do you want to volunteer?"

Style invalid fields with :class="{ 'border-red-500': errors.name }"

Add a success message after a valid submission

Clear form fields and errors after submit -->


<template>
    <div class="max-w-xl mx-auto p-6 bg-white shadow rounded mt-10">
        <h2 class="text-2xl font-bold mb-6">Volunteer Sign-Up</h2>

        <form @submit.prevent="submitForm" class="space-y-5">

            <!-- Full Name -->
            <div>
                <label class="block text-sm font-medium mb-1">Full Name</label>
                <input v-model="form.name" type="text" class="border p-2 w-full rounded" placeholder="John Doe"
                    :class="{ 'border-red-500': errors.name }" />
                <p v-if="errors.name" class="text-red-600 text-sm mt-1">{{ errors.name }}</p>
            </div>
            <!-- Email -->
            <div>
                <label class="block text-sm font-medium mb-1">Email</label>
                <input v-model="form.email" type="email" class="border p-2 w-full rounded"
                    placeholder="Enter your email" :class="{ 'border-red-500': errors.name }" />
                <p v-if="errors.email" class="text-red-600 text-sm mt-1">{{ errors.email }}</p>

            </div>
            <!-- Age -->
            <div>
                <label class="block text-sm font-medium mb-1">Age</label>
                <input v-model="form.age" type="number" class="border p-2 w-full rounded" placeholder="30" />
                <p v-if="errors.age" class="text-red-600 text-sm mt-1">{{ errors.age }}</p>

            </div>
            <!-- Phone -->
            <div>
                <label class="block text-sm font-medium mb-1">Phone Number</label>
                <input v-model="form.phone" type="tel" class="border p-2 w-full rounded" placeholder="123-456-7890"
                    :class="{ 'border-red-500': errors.name }" />
                <p v-if="errors.phone" class="text-red-600 text-sm mt-1">{{ errors.phone }}</p>

            </div>
            <!-- Why Volunteer (textarea) -->
            <div>
                <label class="block text-sm font-medium mb-1">Reasons for Volunterring</label>
                <textarea v-model="form.reason" id="reason" name="reason" rows="4" cols="50"
                    class="border p-2 w-full rounded" placeholder="Tell us why you want to volunteer"
                    :class="{ 'border-red-500': errors.name }">{{ form.reason }}</textarea>
                <p v-if="errors.reason" class="text-red-600 text-sm mt-1">{{ errors.reason }}</p>
            </div>
            <!-- Terms (checkbox) -->
            <div class="flex items-start">
                <input type="checkbox" id="terms" v-model="form.terms" class="mr-2 mt-1"
                    :class="{ 'border-red-500': errors.terms }" />
                <label for="terms" class="text-sm">
                    I agree to the <a href="#" class="text-blue-600 underline">Terms and Conditions</a>
                </label>
            </div>
            <p v-if="errors.terms" class="text-red-600 text-sm mt-1">{{ errors.terms }}</p>

            <!-- Submit button -->
            <button type="submit" class="bg-blue-600 text-white px-4 py-2 rounded hover:bg-blue-700">
                Submit
            </button>
            <!-- Success Message -->
            <p v-if="successMessage" class="mt-4 text-green-600 text-sm">
                {{ successMessage }}
            </p>

        </form>
    </div>
</template>

<script setup>
import { reactive, ref } from 'vue';

const form = reactive({
    name: '',
    email: '',
    age: '',
    phone: '',
    reason: '',
    terms: false
});

const errors = reactive({
    name: '',
    email: '',
    age: '',
    phone: '',
    reason: '',
    terms: ''
});

const successMessage = ref('');

const validateForm = () => {

    const nameRegex = /^[A-Za-z\s]{2,}$/;
    const emailRegex = /^\S+@\S+\.\S+$/;
    const phoneRegex = /^\d{10}$/;

    // Add all your validation logic here using nested ternary logic
    // Example for name:
    errors.name = !form.name
        ? 'Name is required'
        : !nameRegex.test(form.name)
            ? 'Name must be at least 2 letters and only contain letters and spaces'
            : '';

    // (you continue with email, phone, reason, age, terms...)

    // Example for email:
    errors.email = !form.email
        ? "Email is required"
        : !emailRegex.test(form.email)
            ? "Enter a valid email address"
            : "";

    // Example for phone:
    errors.phone = !form.phone
        ? "Phone number is required"
        : !phoneRegex.test(form.phone)
            ? "Phone number must be 10 digits"
            : "";

    // Example for reason:
    errors.reason = !form.reason
        ? "This field is required"
        : form.reason.split(/[.!?]/).filter(s => s.trim().length > 0).length < 2
            ? "Please write at least 2 sentences"
            : "";

    // Example for checkbox:
    errors.terms = !form.terms
        ? "You must agree to the terms and conditions"
        : "";
    return !Object.values(errors).some(e => e);
};

const resetForm = () => {
    form.name = '';
    form.email = '';
    form.age = '';
    form.phone = '';
    form.reason = '';
    form.terms = false;

    Object.keys(errors).forEach(key => errors[key] = '');
};

const submitForm = () => {
    if (!validateForm()) {
        successMessage.value = '';
        return;
    }

    successMessage.value = 'Thank you for signing up to volunteer!';
    resetForm();
};
</script>


