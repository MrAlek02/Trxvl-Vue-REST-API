<script setup>
defineProps({
  offerId: Number,
  title: String,
  subtitle: String,
  description: String,
  textbutton: String,
  image: String,
})
</script>

<template>
  <div class="card | js-about">
    <img class="card-image" v-if="image" :src="image" :alt="title" />
    <div class="card-content">
      <h4 class="card-subtitle">{{ title }}</h4>
      <h2 class="card-title">{{ subtitle }}</h2>
      <p class="card-description">{{ description }}</p>
      <button class="card-button">{{ textbutton }}</button>
    </div>
  </div>
</template>
