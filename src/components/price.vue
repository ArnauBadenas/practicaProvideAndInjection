<template>
    <span>{{ calcPrice(props.price, currency) }}{{ currency }}</span>
</template>
<script setup lang="ts">
import type { Currency } from '@/types/Currency';
import { inject, type Ref } from 'vue';

const props = defineProps<{
    price: number
}>()

const currency: Ref<Currency> = inject<Ref<Currency>>('currency') as Ref<Currency>

//TODO inject currency from app.vue

function calcPrice(price: number, currency: string): number {
    if (currency == "$") {
        return Math.round(((price * 1.09) + Number.EPSILON) * 100) / 100
    }
    //Default is euros
    return price
}
</script>