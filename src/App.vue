<script setup>
import {ref} from "vue";

const product = ref('Socks')
const description = ref('A pair of warm, fuzzy socks')
</script>

<template>
  <h1>
    {{ product }}
  </h1>
  <p>
    {{ description }}
  </p>
</template>

<style scoped>

</style>
