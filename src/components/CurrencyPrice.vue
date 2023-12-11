<script setup lang="ts">
import { computed, inject, defineProps, ref } from "vue";
import type Currency from "../types/Currency";

const props = defineProps<{
    price: number;
}>();
const selectedCurrency: Ref<string> | undefined = inject("selectedCurrency");
const currencies: Array<Currency> | undefined = inject("currencies");

const currencyConversion = {
    "$": 1,
    "€": 0.85,

};

const price = computed(() => {
    const currency = currencies.find((c) => c.icon === selectedCurrency.value);

    if (currency) {
        const conversionRate = currencyConversion[selectedCurrency.value];
        return (props.price * conversionRate).toFixed(2);
    }

    return "";
});
</script>

<template>
    <span>{{ `${price}${selectedCurrency}` }}</span>
</template>
