<script setup>
import { ref, onMounted } from 'vue'

const imageData = ref(null)

const apiPageImageUrl = `${import.meta.env.VITE_API_PAGEIMAGE_URL}`

onMounted(async () => {
  try {
    const response = await fetch(apiPageImageUrl)
    if (!response.ok) throw new Error('Failed to fetch image data')

    imageData.value = await response.json()
  } catch (error) {
    console.error('Error fetching image data:', error)
  }
})
</script>

<template>
  <div class="container">
    <div v-if="imageData" class="image | js-image">
      <img :src="imageData.image" alt="Image" />
      <div class="image-info">
        <h1>{{ imageData.image_title }}</h1>
        <p>{{ imageData.image_text }}</p>
      </div>
    </div>
    <p v-else>Loading...</p>
  </div>
</template>
<style>
.image {
  margin-top: 10%;
  position: relative;
}

.image img {
  width: 100%;
  height: auto;
  border-radius: 27px;
}

.image-info {
  position: absolute;
  bottom: 10%;
  left: 70px;
  right: 70px;
  color: white;
}

.image-info h1 {
  font-size: 5vw;
  font-weight: 700;
}

.image-info p {
  font-size: 2vw;
  font-weight: 400;
}
</style>
