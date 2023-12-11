<template>
    <span>{{ `${formattedPrice} ${currentCurrency}` }}</span>
</template>

<script setup lang="ts">
import { computed, defineProps, inject, type Ref } from "vue";

const props = defineProps<{
    price: number;
}>();

const currentCurrency = inject<Ref<string>>("currency");

const formattedPrice = computed(() => {
    switch (currentCurrency?.value) {
        case "$":
            return props.price.toFixed(2);
        case "€":
            return (props.price * 0.93).toFixed(2);
        case "£":
            return (props.price * 0.79).toFixed(2);
        case "¥":
            return (props.price * 147.11).toFixed(2);
        default:
            return props.price.toFixed(2);
    }
});
</script>

<style scoped>
span {
    margin-right: 5px;
}
</style>
