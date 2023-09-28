<script setup>
const props = defineProps({
    value: String
});
defineEmits(['pressKey']);
</script>
<template>
    <button @click="$emit('pressKey', value)" class="rounded-lg bg-gray-900 text-white w-14 h-14 text-xl hover:bg-gray-700 active:bg-gray-500 focus:outline-none focus:ring focus:ring-blue-300"><slot></slot></button>
</template>