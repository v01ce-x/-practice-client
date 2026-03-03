<script setup>
import { ref } from 'vue'
import AppProduct from './components/AppProduct.vue'

const premium = ref(true)
const cart = ref([])

const handleAddToCart = (id) => {
  cart.value.push(id)
}

const removeFromCart = () => {
  cart.value.splice(cart.value.length - 1, 1)
}
</script>

<template>
  <div id="app">
    <h1>My Store</h1>
    <p>Cart: {{ cart.length }} items</p>
    <AppProduct
      :premium="premium"
      @add-to-cart="handleAddToCart"
      @remove-from-cart="removeFromCart"
    />
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  padding: 2rem;
  max-width: 1200px;
  margin: 0 auto;
}
h1 {
  color: #42b983;
}
</style>
