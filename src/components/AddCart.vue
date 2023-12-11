<template>
    <p>
        {{ info.name }}<Price :price="info.price" />
        <button @click="$emit('@addToCart', info)" type="button">
            Add to Cart
        </button>
    </p>
</template>

<script setup lang="ts">
import Price from "./Price.vue";
defineProps<{
    info: any;
}>();

defineEmits<{
    "@addToCart": [info: { name: string; price: number }];
}>();
</script>

<style scoped>
p {
    margin: 10px;
}
</style>
