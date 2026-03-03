<script setup>
import { ref } from 'vue'

const emit = defineEmits(['review-submitted'])

const name = ref(null)
const review = ref(null)
const rating = ref(null)
const errors = ref({
  name: [],
  review: [],
  rating: [],
})

const validate = () => {
  errors.value = { name: [], review: [], rating: [] }
  let isValid = true

  if (!name.value) {
    errors.value.name.push('Name required.')
    isValid = false
  }
  if (!review.value) {
    errors.value.review.push('Review required.')
    isValid = false
  }
  if (!rating.value) {
    errors.value.rating.push('Rating required.')
    isValid = false
  }

  return isValid
}

const onSubmit = () => {
  if (validate()) {
    const productReview = {
      name: name.value,
      review: review.value,
      rating: rating.value,
    }
    emit('review-submitted', productReview)

    name.value = null
    review.value = null
    rating.value = null
  }
}
</script>

<template>
  <form class="review-form" @submit.prevent="onSubmit">
    <p>
      <label for="name">Name:</label>
      <input
        id="name"
        v-model="name"
        placeholder="name"
        :style="{ border: errors.name[0] ? '1px solid red' : '1px solid black' }"
      >
      <span v-show="errors.name[0]" style="color: red">{{ errors.name[0] }}</span>
    </p>
    <p>
      <label for="review">Review:</label>
      <textarea
        id="review"
        v-model="review"
        :style="{ border: errors.review[0] ? '1px solid red' : '1px solid black' }"
      ></textarea>
      <span v-show="errors.review[0]" style="color: red">{{ errors.review[0] }}</span>
    </p>
    <p>
      <label for="rating">Rating:</label>
      <select
        id="rating"
        v-model.number="rating"
        :style="{ border: errors.rating[0] ? '1px solid red' : '1px solid black' }"
      >
        <option :value="5">5</option>
        <option :value="4">4</option>
        <option :value="3">3</option>
        <option :value="2">2</option>
        <option :value="1">1</option>
      </select>
      <span v-show="errors.rating[0]" style="color: red">{{ errors.rating[0] }}</span>
    </p>
    <p>
      <input type="submit" value="Submit">
    </p>
  </form>
</template>

<style scoped>
.review-form {
  max-width: 500px;
  margin: 1rem 0;
}
.review-form p {
  margin: 0.5rem 0;
}
.review-form label {
  display: block;
  margin-bottom: 0.25rem;
}
.review-form input,
.review-form textarea,
.review-form select {
  width: 100%;
  padding: 0.5rem;
  box-sizing: border-box;
}
.review-form input[type="submit"] {
  width: auto;
  padding: 0.5rem 1.5rem;
  cursor: pointer;
}
</style>
