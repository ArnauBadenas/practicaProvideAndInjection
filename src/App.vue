<script setup lang="ts">
import { type Ref, ref } from 'vue';
import type { Order } from './types/Order';
import order from './components/order.vue';
const orders: Ref<Order[]> = ref([{ name: "Hamburger 🍔.", price: 5 },
{ name: "Cheeseburger 🧀", price: 6 },
{ name: "Impossible Burger 🥕", price: 7 },
{ name: "Fries 🍟", price: 2 }])

const orderTitle: Ref<string> = ref("Tom's Dinner")
const cart: Ref<Order | undefined> = ref()
</script>

<template>
  <!--  -->
  <h1 id="order-title">{{ orderTitle }}</h1>
  <input type="text" name="order-title" id="order-title" v-model="orderTitle">
  <select>
    <option value="€">€</option>
    <option value="$">$</option>
  </select>

  <order v-for="order in orders" :key="order.name" :order="order"></order>
</template>

<style scoped></style>
