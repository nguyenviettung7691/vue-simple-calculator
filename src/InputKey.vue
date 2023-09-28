<script setup>
import KeyButton from "@/KeyButton.vue";
const props = defineProps({
    value: String
});
defineEmits(['pressKey']);
</script>
<template>
    <KeyButton :value="value" @press-key="$emit('pressKey', value)">{{ value }}</KeyButton>
</template>