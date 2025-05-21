<!-- Step 4: Reusable Form Components -->

<!-- <BaseInput
  label="Email"
  id="email"
  type="email"
  v-model="form.email"
  :error="errors.email"
  placeholder="you@example.com"
/> -->

<template>
    <div>
        <label :for="id" class="block text-sm font-medium mb-1">
            {{ label }}
        </label>

        <input :id="id" :type="type" :placeholder="placeholder" :value="modelValue"
            @input="$emit('update:modelValue', $event.target.value)"
            class="w-full px-4 py-2 rounded border transition-colors focus:outline-none focus:ring-2" :class="[
                error
                    ? 'border-red-500 focus:ring-red-500'
                    : 'border-gray-300 focus:ring-primary-500 focus:border-primary-500'
            ]" />


        <p v-if="error" class="text-red-600 text-sm mt-1">{{ error }}</p>
    </div>
</template>

<script setup>
defineProps({
    label: String,
    id: String,
    modelValue: [String, Number],
    placeholder: String,
    type: {
        type: String,
        default: 'text'
    },
    error: {
        type: String,
        default: ''
    }
});
</script>