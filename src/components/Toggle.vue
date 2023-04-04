<script setup lang="ts">
defineProps({
    toggled: Boolean,
})

defineEmits(["toggle"])
</script>

<template>
    <button type="button" @click="event => $emit("toggle", event)"><slot></slot></button>
</template>