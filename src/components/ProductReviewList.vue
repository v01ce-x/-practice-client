<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  reviews: {
    type: Array,
    required: true
  }
})

const currentFilter = ref(null)
const filterOptions = [null, 1, 2, 3, 4, 5]

const filteredReviews = computed(() => {
  if (currentFilter.value) {
    return props.reviews.filter(r => r.rating === currentFilter.value)
  }
  return props.reviews
})
</script>

<template>
  <div>
    <select name="filter" v-model.number="currentFilter">
      <option
        v-for="(option, index) in filterOptions"
        :key="index"
        :value="option"
      >
        {{ option ?? 'Не важно' }}
      </option>
    </select>

    <p v-if="!filteredReviews.length">There are no reviews yet.</p>

    <ul>
      <li v-for="(review, idx) in filteredReviews" :key="idx">
        <p>{{ review.name }}</p>
        <p>Rating: {{ review.rating }}</p>
        <p>{{ review.review }}</p>
        <template v-if="review.recommendations">
          <p>{{ review.recommendations ? 'Рекомендую' : 'Не рекомендую' }} к покупке</p>
        </template>
      </li>
    </ul>
  </div>
</template>

<style scoped>
select {
  margin-bottom: 1rem;
  padding: 0.5rem;
}
ul {
  list-style: none;
  padding: 0;
}
li {
  border-bottom: 1px solid #ccc;
  padding: 1rem 0;
}
</style>
