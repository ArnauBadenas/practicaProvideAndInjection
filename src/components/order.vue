<template>
    <section class="order">
        <p>{{ order.name }} </p>
        <Price :price="order.price"></Price>
        <input type="button" value="Add to cart">
    </section>
</template>

<script setup lang="ts">
import type { Order } from '../types/Order'
import Price from './price.vue';
const props = defineProps<{
    order: Order
}>()
//TODO add to cart with an emit
</script>
<style scoped>
    .order{
        display: flex;
    }
</style>