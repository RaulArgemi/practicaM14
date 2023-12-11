<template>
    <div>
        <h1>{{ name }}</h1>
        <input v-model="name" type="text" />
        <button @click="añadirOrden">Place Order</button>
    </div>
    <div>
        <div>
            <label for="currency">Currency</label>
            <select name="currency" id="currency" v-model="selectedCurrency">
                <option v-for="currency in currencies" :key="currency.icon" :value="currency.icon">
                    {{ currency.name }}
                </option>
            </select>
        </div>
        <ul>
            <Order v-for="product in products" :key="product.name" :product="product" :aniadirAlCarrito="aniadirAlCarrito" @@add-to-cart="(product: Product) => aniadirAlCarrito(product)" />
        </ul>
    </div>
</template>

<script setup lang="ts">
import { ref, reactive, provide } from "vue";

import Product from "./types/Product";
import Currency from "./types/Currency";

import Order from "./components/Order.vue";

const products = reactive<Array<Product>>([
    { name: "Hamburger 🍔", price: 5 },
    { name: "Cheeseburger 🧀", price: 6 },
    { name: "Impossible Burger 🥕", price: 7 },
    { name: "Fries 🍟", price: 2 },
]);

const currencies = reactive<Array<Currency>>([
    {
        icon: "$",
        name: "Dollars ($)",
        convert: 1,
    },
    {
        icon: "€",
        name: "Euros ($)",
        convert: 0.92,
    },
]);

const selectedCurrency = ref<string>("$")
const name = ref<string>("The Snazzy Burger");
const cart = reactive<Array<Product | null>>([]);

function añadirOrden(): void {
    window.alert(`Your order ${name.value} has been placed!`);
}

function aniadirAlCarrito(product: Product): void {
    cart.push(product);
    window.alert(cart.map((p) => p.name));
}

provide("selectedCurrency", selectedCurrency)
provide("currencies", currencies)
</script>

<style>

body{
    text-align: center;
}

ul, li{
    list-style: none;
}

</style>