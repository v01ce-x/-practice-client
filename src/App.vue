<script setup>
import {reactive, ref} from "vue";

import ProductImage from '@/assets/images/vmSocks-green-onWhite.jpeg'

const product = reactive({
  title: 'Socks',
  description: 'A pair of warm, fuzzy socks',
  image: ProductImage,
  altText: "A pair of socks",
  inStock: true,
  onSale: true,
  inventory: 100
})

const href = ref('https://www.amazon.com/s/ref=nb_sb_noss?url=search-alias%3Daps&field-keywords=socks')
</script>

<template>
  <div>
    <img :src="product.image" :alt="product.altText" />
    <h1>{{ product.title }}</h1>
    <p>{{ product.description }}</p>
    <p v-if="product.inventory > 10">In stock</p>
    <p v-else-if="product.inventory <= 10 && product.inventory > 0">Almost sold out!</p>
    <p v-else>Out of stock</p>
    <span v-show="product.onSale">On Sale</span>
  </div>

  <a :href="href">More products like this</a>
</template>

<style scoped>

</style>
