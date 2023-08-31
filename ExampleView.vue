<script setup>
import { ref } from 'vue'

const itemId = ref(0)
const shoppingitem = ref('')
const shoppinglist = ref([])
const shopped = ref(false)

const cart = ref([]) // in this i have creates a list of item inside the cart

function addItem() {
    shoppinglist.value.push({
        id: itemId.value++,
        item: shoppingitem.value,
        status: shopped.value
    })
    shoppingitem.value = ""
}

function removeItem(i) {
    shoppinglist.value = shoppinglist.value.filter((t) => t !== i)
}

function addToCart(item) {
    cart.value.push(item) // option that can add item into cart
}

</script>

<template>
<div>
    <h1>My Shopping List</h1>

    <input type="text" v-model="shoppingitem">
    <button @click="addItem">Add Item</button>
    
    <!-- print the item in the cart if pressing add to cart -->
    <div class="cart">
        <h2>Cart</h2>
        <ul>
            <li v-for="item in cart" :key="item.id">{{ item.item }}</li>
        </ul>
    </div>
    
    <h2>Shopping List</h2>
    <ol>
        <li v-for="i in shoppinglist">
            <input type="checkbox" v-model="i.status">
            <span :class="{ done: i.status }">{{ i.item }}</span>
            <button @click="removeItem(i)">REMOVE ITEM</button>
            <button @click="addToCart(i)">Add to Cart</button>
        </li>
    </ol>
</div>
</template>

<style scoped>
    .done {
        text-decoration: line-through;
    }

    .cart {
        margin-top: 20px;
    }

    div {
        width: 100%;
        height: 400px;
        background-color: bisque;
    }
</style>
