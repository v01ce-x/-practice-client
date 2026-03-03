<script setup>
import { ref } from 'vue'
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
  selectedTab.value = 'Reviews'
}

const closeModal = () => {
  selectedTab.value = 'Reviews'
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

    <Teleport to="#modal">
      <Transition name="modal">
        <div
          v-if="selectedTab === 'Make a Review'"
          class="modal-overlay"
          @click="closeModal"
        >
          <div class="modal-container" @click.stop>
            <button class="close-btn" @click="closeModal">×</button>
            <ProductReview @review-submitted="handleReviewSubmit" />
          </div>
        </div>
      </Transition>
    </Teleport>

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
.modal-enter-active,
.modal-leave-active {
  transition: opacity 0.2s ease;
}
.modal-enter-from,
.modal-leave-to {
  opacity: 0;
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 999;
}

.modal-container {
  position: relative;
  background: white;
  padding: 2rem;
  border-radius: 8px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
  z-index: 1000;
  max-width: 750px;
  width: 90%;
}

.close-btn {
  position: absolute;
  top: 10px;
  right: 15px;
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
  color: #666;
  padding: 0;
  line-height: 1;
}

.close-btn:hover {
  color: #000;
}

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
