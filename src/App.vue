<script setup>
import {reactive, ref} from "vue";

import ProductImage from '@/assets/images/vmSocks-green-onWhite.jpeg'
import ProductImage2 from '@/assets/images/туфли.jpeg'

const product = reactive({
  title: 'Socks',
  description: 'A pair of warm, fuzzy socks',
  image: ProductImage,
  altText: "A pair of socks",
  inStock: true,
  onSale: true,
  inventory: 100,
  cart: 0,
  details: ['80% cotton', '20% polyester', 'Gender-neutral'],
  variants: [
    {
      variantId: 2234,
      variantColor: 'green',
      variantImage: ProductImage,
    },
    {
      variantId: 2235,
      variantColor: 'blue',
      variantImage: ProductImage2,
    }
  ],
  sizes: ['S', 'M', 'L', 'XL', 'XXL', 'XXXL'],
})

const href = ref('https://www.amazon.com/s/ref=nb_sb_noss?url=search-alias%3Daps&field-keywords=socks')

const addToCart = () => {
  product.cart += 1
}

const deleteToCart = () => {
  product.cart -= 1
}

const updateProduct = (variantImages) => {
  product.image = variantImages
}
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
    <ul>
      <li v-for="detail in product.details">{{ detail }}</li>
    </ul>
    <div v-for="variant in product.variants" :key="variant.variantId">
      <p>{{ variant.variantColor }}</p>
    </div>
    <div>
      <p v-for="size of product.sizes">
        {{ size }}
      </p>
    </div>
    <div>
      <p>Cart({{ product.cart }})</p>
    </div>
  </div>

  <div v-for="variant in product.variants" :key="variant.variantId">
    <p @mouseover="updateProduct(variant.variantImage)">
      {{ variant.variantColor }}
    </p>
  </div>

  <button @click="addToCart">Add to cart</button>
  <button @click="deleteToCart">Delete to cart</button>
  <a :href="href">More products like this</a>
</template>

<style scoped>

</style>
