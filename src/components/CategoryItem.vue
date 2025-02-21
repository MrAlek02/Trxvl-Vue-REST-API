<script setup>
import { ref, onMounted, defineProps } from 'vue'

const props = defineProps({
  categoryId: Number,
})

const category = ref(null)

const fetchCategory = async () => {
  try {
    const response = await fetch(
      `http://localhost/trxvl/wp-json/trxvl-ruta/v1/categories/${props.categoryId}`,
    )
    if (!response.ok) throw new Error('Failed to fetch category')

    category.value = await response.json()
  } catch (error) {
    console.error('Error fetching category:', error)
  }
}

onMounted(fetchCategory)
</script>

<template>
  <div v-if="category" class="category">
    <img v-if="category.image" :src="category.image" :alt="category.name" />
    <h1>{{ category.name }}</h1>
  </div>
  <p v-else>Loading...</p>
</template>
