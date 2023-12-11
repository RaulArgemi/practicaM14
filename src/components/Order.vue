<template>
    <li>
        <p>
            {{ product.name }}
        </p>
        <CurrencyPrice :price="product.price" />
        <button @click="$emit('@addToCart', product)">Añadir al carrito</button>
    </li>
</template>

<script setup lang="ts">
import type Product from '../types/Product';
import type Currency from '../types/Currency';
import CurrencyPrice from '../components/CurrencyPrice.vue'

defineProps<{ product: Product; }>()
defineEmits<{ "@addToCart": [product: Product] }>()
</script>