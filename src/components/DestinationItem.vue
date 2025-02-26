<script setup>
import { defineProps, ref, onMounted } from 'vue'

const props = defineProps({
  postId: Number,
  title: String,
  image: String,
})

const isLoading = ref(true)

onMounted(() => {
  setTimeout(() => {
    isLoading.value = false
  }, 3000)
})
</script>

<template>
  <div v-if="isLoading">
    <div class="skeleton-box skeleton-image"></div>
  </div>

  <div v-else class="destination | js-destinations">
    <img :src="image" :alt="title" />
    <div class="destination-info">
      <h2>{{ title }}</h2>
    </div>
  </div>
</template>

<style scoped>
.skeleton-image {
  width: 350px;
  height: 200px;
}

.skeleton-box {
  background: #e0e0e0;
  border-radius: 8px;
  animation: pulse 1.5s infinite ease-in-out;
}

@keyframes pulse {
  0% {
    background-color: #e0e0e0;
  }
  50% {
    background-color: #f0f0f0;
  }
  100% {
    background-color: #e0e0e0;
  }
}
</style>
