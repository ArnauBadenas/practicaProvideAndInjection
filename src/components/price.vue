<template>
    <span>{{ props.price }}</span>
</template>
<script setup lang="ts">
const props = defineProps<{
    price: number
}>()

//TODO inject currency from app.vue

function calcPrice(price: number, currency: string): number {
    return 0
}
</script>