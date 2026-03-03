<script setup>
import { ref, computed } from 'vue'
import ProductTabs from './ProductTabs.vue'

import vmSocksBlueOnWhite from '@/assets/vmSocks-blue-onWhite.jpg'
import vmSocksGreenOnWhite from '@/assets/vmSocks-green-onWhite.jpg'

const props = defineProps({
  premium: {
    type: Boolean,
    required: true
  }
})

const emit = defineEmits(['add-to-cart', 'remove-from-cart'])

const product = 'Socks'
const brand = 'Vue Mastery'
const altText = 'A pair of socks'
const details = ['80% Cotton', '20% Polyester', 'Gender-neutral']
const selectedVariant = ref(0)
const reviews = ref([])

const variants = [
  {
    variantId: 2234,
    variantColor: 'green',
    variantImage: vmSocksGreenOnWhite,
    variantQuantity: 0,
  },
  {
    variantId: 2235,
    variantColor: 'blue',
    variantImage: vmSocksBlueOnWhite,
    variantQuantity: 10,
  },
]

const title = computed(() => `${product} ${brand}`)
const image = computed(() => variants[selectedVariant.value].variantImage)
const inStock = computed(() => variants[selectedVariant.value].variantQuantity > 0)
const shipping = computed(() => props.premium ? "Free" : "2.99")

const addToCart = () => {
  const id = variants[selectedVariant.value].variantId
  emit('add-to-cart', id)
}

const removeFromCart = () => {
  const id = variants[selectedVariant.value].variantId
  emit('remove-from-cart', id)
}

const updateProduct = (index) => {
  selectedVariant.value = index
}

const handleReviewSubmit = (review) => {
  reviews.value.push(review)
}
</script>

<template>
  <div class="product">
    <div class="product-image">
      <img :src="image" :alt="altText">
    </div>
    <div class="product-info">
      <h1>{{ title }}</h1>
      <p v-if="inStock">In stock</p>
      <p v-else>Out of Stock</p>

      <div class="flex">
        <div
          class="color-box"
          v-for="(variant, index) in variants"
          :key="variant.variantId"
          :style="{ backgroundColor: variant.variantColor }"
          @mouseover="updateProduct(index)"
        ></div>

        <div class="buttons">
          <button
            @click="addToCart"
            :disabled="!inStock"
            :class="{ disabledButton: !inStock }"
          >
            Add to cart
          </button>

          <button
            @click="removeFromCart"
            :disabled="!inStock"
            :class="{ disabledButton: !inStock }"
          >
            Remove from cart
          </button>
        </div>
      </div>

      <ProductTabs
        :reviews="reviews"
        :details="details"
        :shipping="shipping"
        @review-submitted="handleReviewSubmit"
      />
    </div>
  </div>
</template>

<style scoped>
.product {
  display: flex;
  gap: 2rem;
  max-width: 800px;
  margin: 2rem auto;
}
.product-image img {
  max-width: 300px;
  border: 1px solid #ccc;
}
.product-info {
  flex: 1;
}
.color-box {
  width: 30px;
  height: 30px;
  display: inline-block;
  margin-right: 0.5rem;
  cursor: pointer;
  border: 1px solid #ccc;
}
button {
  width: 170px;
  padding: 0.75rem 1.5rem;
  cursor: pointer;
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 4px;
  margin: 0;
}
.buttons {
  display: flex;
  align-items: center;
  gap: 10px;
}
.disabledButton {
  opacity: 0.5;
  cursor: not-allowed;
  background-color: #ccc;
}
.flex {
  display: flex;
  align-items: center;
  margin: 10px 0;
}
</style>
