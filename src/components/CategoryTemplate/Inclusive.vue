<script setup>
import { ref, watch } from 'vue'
import InclusiveItem from './Items.vue'

import { register } from 'swiper/element/bundle'
register()

const posts = ref([])

const props = defineProps({
  categoryId: { type: Number, required: true },
})

watch(
  () => props.categoryId,
  async (newCategoryId) => {
    try {
      const response = await fetch(
        `http://localhost/trxvl/wp-json/trxvl/v1/categories/inclusive/${newCategoryId}`,
      )
      if (!response.ok) throw new Error('Failed to fetch posts')

      posts.value = await response.json()
    } catch (error) {
      console.error('Error fetching posts:', error)
    }
  },
)
</script>

<template>
  <div class="container">
    <h1 class="| js-package">All Inclusive Packages!</h1>
  </div>
  <div class="package">
    <swiper-container
      :slides-per-view="'auto'"
      :loop="true"
      :space-between="20"
      direction="horizontal"
    >
      <swiper-slide class="swiper-slide" v-for="post in posts" :key="post.id">
        <InclusiveItem
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
      </swiper-slide>
    </swiper-container>
  </div>
</template>
<style></style>
