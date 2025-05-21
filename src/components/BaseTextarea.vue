<template>
    <div class="mb-4">
        <label :for="id" class="block text-sm font-medium mb-1">
            {{ label }}
        </label>

        <textarea :id="id" :name="id" :placeholder="placeholder" :value="modelValue"
            @input="$emit('update:modelValue', $event.target.value)" :rows="rows" :cols="cols"
            class="border p-2 w-full rounded" :class="{ 'border-red-500': error }"></textarea>

        <p v-if="error" class="text-red-600 text-sm mt-1">{{ error }}</p>
    </div>
</template>

<script setup>
defineProps({
    label: String,
    id: String,
    modelValue: String,
    placeholder: String,
    rows: {
        type: [Number, String],
        default: 4
    },
    cols: {
        type: [Number, String],
        default: 50
    },
    error: {
        type: String,
        default: ''
    }
});
</script>


<!-- 
<BaseTextarea
  id="reason"
  label="Reasons for Volunteering"
  v-model="form.reason"
  :error="errors.reason"
  placeholder="Tell us why you want to volunteer"

  ****To control rows and columns****
  :rows="6"

  ****Don't always need this because of the w-full****
    :cols="60"
/>
-->