<template>
    <form class="order" @submit.prevent="handleSubmitOrder()">
        <label class="name">{{ order.name }} </label>
        <Price class="price" :price="order.price"></Price>
        <input type="submit" value="Add to cart">
    </form>
</template>

<script setup lang="ts">
import type { Order } from '../types/Order'
import Price from './price.vue';
const props = defineProps<{
    order: Order
}>()
const emit = defineEmits<{
    (e: "submitOrder", order: Order): void
}>();
function handleSubmitOrder(): void {
    emit('submitOrder', props.order)
}
</script>
<style scoped>
.order {
    display: flex;
    justify-content: space-between;
    width: 300px;
}

.name {
    width: 70%;
}

.price {
    width: 20%;
    display: flex;
    justify-content: end;
    padding: 0 10px;
}
</style>