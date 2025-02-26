<script setup>
import { ref, onMounted } from 'vue'
import Honeymoon from './Items.vue'

import { register } from 'swiper/element/bundle'
register()

const posts = ref([])

onMounted(async () => {
  try {
    const response = await fetch('http://localhost/trxvl/wp-json/trxvl/v1/categories/honeymoon/22')
    if (!response.ok) throw new Error('Failed to fetch posts')

    posts.value = await response.json()
  } catch (error) {
    console.error('Error fetching posts:', error)
  }
})
</script>

<template>
  <div class="container">
    <h1 class="| js-recently">Recetly Viewed</h1>
  </div>
  <div class="recently-cards">
    <div v-for="post in posts" :key="post.id" class="item">
      <Honeymoon
        :id="post.id"
        :title="post.title"
        :thumbnail="post.thumbnail"
        :rating="post.rating"
        :star="post.star"
        :stays="post.stays"
        :flights_text="post.flights_text"
        :flights="post.flights"
        :hotels_text="post.hotels_text"
        :hotels="post.hotels"
        :transfers_text="post.transfers_text"
        :transfers="post.transfers"
        :activities_text="post.activities_text"
        :activities="post.activities"
        :list="post.list"
        :price_text="post.price_text"
        :price_sale_text="post.price_sale_text"
        :per="post.per"
      />
    </div>
  </div>
</template>
<style></style>
