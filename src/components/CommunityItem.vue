<script setup>
defineProps({
  communityId: Number,
  title: String,
  description: String,
  image: String,
})
</script>

<template>
  <div class="card-com | js-community">
    <img class="card-com-image" v-if="image" :src="image" :alt="title" />
    <div class="card-com-content">
      <h2 class="card-com-title">{{ title }}</h2>
      <div class="card-com-description">
        <p v-html="description"></p>
      </div>
    </div>
  </div>
</template>
