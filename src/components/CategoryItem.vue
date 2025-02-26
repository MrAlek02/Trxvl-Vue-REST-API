<script setup>
import { ref, onMounted, defineProps } from 'vue'

const props = defineProps({
  categoryId: Number,
})

const category = ref(null)
const isLoading = ref(true)

const fetchCategory = async () => {
  try {
    const response = await fetch(
      `http://localhost/trxvl/wp-json/trxvl-ruta/v1/categories/${props.categoryId}`,
    )
    if (!response.ok) throw new Error('Failed to fetch category')

    const data = await response.json()

    setTimeout(() => {
      category.value = data
      isLoading.value = false
    }, 3000)
  } catch (error) {
    console.error('Error fetching category:', error)
    isLoading.value = false
  }
}

onMounted(fetchCategory)
</script>

<template>
  <div v-if="isLoading" class="category-skeleton">
    <div class="skeleton-box skeleton-image"></div>
    <div class="skeleton-box skeleton-text"></div>
  </div>
  <div v-else-if="category" class="category">
    <img v-if="category.image" :src="category.image" :alt="category.name" />
    <h1>{{ category.name }}</h1>
  </div>
</template>
<style scoped>
.category-skeleton {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
  width: 150px;
  padding: 10px;
}
.skeleton-box {
  background: #e0e0e0;
  border-radius: 8px;
  animation: pulse 1.5s infinite ease-in-out;
}

.skeleton-image {
  width: 50px;
  height: 50px;
}

.skeleton-text {
  width: 80px;
  height: 20px;
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
