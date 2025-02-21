<script setup>
import { defineProps } from 'vue'

defineProps({
  postId: Number,
  title: String,
  image: String,
})
</script>

<template>
  <div class="destination | js-destinations">
    <img v-if="image" :src="image" :alt="title" />
    <div class="destination-info">
      <h2>{{ title }}</h2>
    </div>
  </div>
</template>
