<script setup>
import { ref, onMounted } from 'vue'
import DestinationItem from './DestinationItem.vue'

import { register } from 'swiper/element/bundle'
register()

const posts = ref([])

onMounted(async () => {
  try {
    const response = await fetch('http://localhost/trxvl/wp-json/trxvl-ruta/v1/posts')
    if (!response.ok) throw new Error('Failed to fetch posts')

    posts.value = await response.json()
  } catch (error) {
    console.error('Error fetching posts:', error)
  }
})
</script>

<template>
  <div class="container">
    <div class="hero-subtitle | js-destinations">
      <h1>Top Vacation Destinations</h1>
    </div>
  </div>
  <div class="destinations">
    <swiper-container
      :slides-per-view="'auto'"
      :loop="true"
      :space-between="20"
      direction="horizontal"
    >
      <swiper-slide class="swiper-slide" v-for="post in posts" :key="post.id">
        <DestinationItem :postId="post.id" :title="post.title" :image="post.image" />
      </swiper-slide>
    </swiper-container>
  </div>
</template>
<style>
.swiper-slide {
  width: fit-content !important;
}

.destinations {
  margin-left: 10%;
}

.destination {
  position: relative;
}

.destination img {
  border-radius: 9px;
}

.destination-info {
  position: absolute;
  bottom: 0;
  left: 0;
  padding: 10px;
  color: white;
}

.destination-info h2 {
  margin: 0;
}

@media (max-width: 1200px) {
  .destination img {
    width: 230px;
  }
  .subtitle h1 {
    font-size: 24px;
  }
  .hero-subtitle h1 {
    font-size: 24px;
  }
}
</style>
