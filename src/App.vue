<template>
    <div class="container">
        <header>
            <h1>{{ orderName }}</h1>
            <section>
                <input class="order" v-model="orderName" type="text" />
                <button @click="placeOrder" type="button">Place Order</button>
            </section>
        </header>

        <main>
            <div>
                <label for="currency">Currency</label>
                <select v-model="currency" name="currency" id="currency">
                    <option value="$">USD ($)</option>
                    <option value="€">EUR (€)</option>
                    <option value="£">GBP (£)</option>
                    <option value="¥">JPY (¥)</option>
                </select>
            </div>
            <section class="menu">
                <AddCart
                    @@addToCart="(product) => addToCart(product)"
                    v-for="(product, index) in products"
                    :info="product"
                    :key="index"
                />
            </section>
        </main>
    </div>
</template>

<script setup lang="ts">
import { ref, reactive, provide, type Ref } from "vue";
import AddCart from "@/components/AddCart.vue";

const orderName = ref("Vuerguer King");
const currency = ref("$");
const cart: Ref<{ name: string; price: number }[]> = ref([]);
const products = reactive([
    { name: " Hamburger 🍔 ", price: 5.0 },
    { name: " Cheeseburger 🧀 ", price: 6.0 },
    { name: " Impossible Burger 🥕 ", price: 7.0 },
    { name: " Fries 🍟 ", price: 2.0 },
]);

const placeOrder = (): void => {
    cart.value = [];
    alert(`Your order has been placed.`);
};

const addToCart = (product: { name: string; price: number }): void => {
    cart.value.push(product);
    alert(
        cart.value
            .map((product: { name: string; price: number }) => product.name)
            .join(", ")
    );
};

provide("currency", currency);
</script>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
    margin: 0;
}

header,
main {
    text-align: center;
}

main {
    margin-top: 20px;
}

.order {
    margin-right: 5px;
}

.menu {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
}
</style>
