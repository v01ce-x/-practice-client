<script setup>
import { ref } from 'vue'
// ВАЖНО: ProductReview (без s на конце!)
import ProductReview from './ProductReview.vue'
import ProductReviewList from './ProductReviewList.vue'

const props = defineProps({
  reviews: { type: Array, required: false },
  shipping: { type: String, required: true },
  details: { type: Array, required: true }
})

const emit = defineEmits(['review-submitted'])

const tabs = ['Reviews', 'Make a Review', 'Shipping', 'Details']
const selectedTab = ref('Reviews')

const handleReviewSubmit = (review) => {
  emit('review-submitted', review)
}
</script>

<template>
  <div>
    <ul class="tabs-list">
      <li
        class="tab"
        :class="{ activeTab: selectedTab === tab }"
        v-for="tab in tabs"
        :key="tab"
        @click="selectedTab = tab"
      >
        {{ tab }}
      </li>
    </ul>

    <div v-show="selectedTab === 'Reviews'">
      <ProductReviewList :reviews="reviews" />
    </div>
    <div v-show="selectedTab === 'Make a Review'">
      <ProductReview @review-submitted="handleReviewSubmit" />
    </div>
    <div v-show="selectedTab === 'Shipping'">
      <p>Shipping: {{ shipping }}</p>
    </div>
    <div v-show="selectedTab === 'Details'">
      <ul>
        <li v-for="(detail, idx) in details" :key="idx">{{ detail }}</li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.tabs-list {
  display: flex;
  gap: 0.5rem;
  list-style: none;
  padding: 0;
  margin-bottom: 1rem;
  border-bottom: 2px solid #ccc;
}
.tab {
  cursor: pointer;
  padding: 0.5rem 1rem;
  border: 1px solid transparent;
  border-bottom: none;
}
.tab:hover {
  background-color: #f0f0f0;
}
.activeTab {
  font-weight: bold;
  border: 1px solid #ccc;
  border-bottom: 2px solid white;
  background-color: white;
  margin-bottom: -2px;
}
</style>
