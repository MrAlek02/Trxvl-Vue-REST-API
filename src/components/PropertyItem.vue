<script setup>
import { defineProps, ref, onMounted, onUnmounted } from 'vue'

const props = defineProps({
  property: Object,
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
      <div class="skeleton-box skeleton-image"></div>
    </div>

    <div v-else-if="property" class="destination | js-property">
      <img v-if="property.image" :src="property.image" :alt="property.name" />
      <div class="destination-info">
        <h2>{{ property.name }}</h2>
      </div>
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
