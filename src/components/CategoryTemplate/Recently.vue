<script setup>
import { ref, watch } from 'vue'
import RecentlyItem from './RecentlyItem.vue'

const posts = ref([])

const props = defineProps({
  categoryId: {
    type: Number,
    required: true,
  },
})

watch(
  () => props.categoryId,
  async (newCategoryId) => {
    if (!newCategoryId) return

    const apiUrl = `${import.meta.env.VITE_API_RECENTLY_URL}/${newCategoryId}`

    try {
      const response = await fetch(apiUrl)
      if (!response.ok) throw new Error('Failed to fetch posts')

      posts.value = await response.json()
    } catch (error) {
      console.error('Error fetching posts:', error)
    }
  },
  { immediate: true },
)
</script>
<template>
  <div class="container">
    <h1 class="| js-recently">Recetly Viewed</h1>
  </div>
  <div class="recently-cards">
    <div v-for="post in posts" :key="post.id">
      <RecentlyItem
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
<style>
.recently-cards {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  margin-left: 10%;
}

.recently-cards .card-mtn {
  margin-right: 20px;
}
</style>
