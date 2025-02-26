<script setup>
import { defineProps, ref, onMounted, onUnmounted } from 'vue'

defineProps({
  offerId: Number,
  title: String,
  subtitle: String,
  description: String,
  textbutton: String,
  image: String,
})

const isLoading = ref(false)
const observer = ref(null)
const sectionRef = ref(null)

const startLoading = () => {
  isLoading.value = true
  setTimeout(() => {
    isLoading.value = false
  }, 3000)
}

onMounted(() => {
  observer.value = new IntersectionObserver(
    (entries) => {
      if (entries[0].isIntersecting) {
        startLoading()
        observer.value.disconnect()
      }
    },
    { threshold: 0.2 },
  )

  if (sectionRef.value) {
    observer.value.observe(sectionRef.value)
  }
})

onUnmounted(() => {
  if (observer.value) observer.value.disconnect()
})
</script>

<template>
  <div ref="sectionRef">
    <div v-if="isLoading">
      <div class="skeleton-image skeleton-box"></div>
    </div>

    <div v-else class="card | js-about">
      <img class="card-image" v-if="image" :src="image" :alt="title" />
      <div class="card-content">
        <h4 class="card-subtitle">{{ title }}</h4>
        <h2 class="card-title">{{ subtitle }}</h2>
        <p class="card-description">{{ description }}</p>
        <button class="card-button">{{ textbutton }}</button>
      </div>
    </div>
  </div>
</template>
<style scoped>
.skeleton-image {
  width: 700px;
  height: 300px;
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
