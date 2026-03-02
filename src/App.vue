<script setup>
import {reactive, ref} from "vue";

import ProductImage from '@/assets/images/vmSocks-green-onWhite.jpeg'

const product = reactive({
  title: 'Socks',
  description: 'A pair of warm, fuzzy socks',
  image: ProductImage,
  altText: "A pair of socks"
})

const href = ref('https://www.amazon.com/s/ref=nb_sb_noss?url=search-alias%3Daps&field-keywords=socks')
</script>

<template>
  <div>
    <h1>{{ product.title }}</h1>
    <p>{{ product.description }}</p>
    <img :src="product.image" :alt="product.altText" />
  </div>

  <a :href="href">like this</a>
</template>

<style scoped>

</style>
