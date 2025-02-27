<script setup>
import { ref, onMounted } from 'vue'
import CommunityItem from './CommunityItem.vue'
import { register } from 'swiper/element/bundle'

register()

const community = ref([])

const apiCommunityUrl = `${import.meta.env.VITE_API_COMMUNITY_URL}`

onMounted(async () => {
  try {
    const response = await fetch(apiCommunityUrl)
    if (!response.ok) throw new Error('Failed to fetch community data')

    community.value = await response.json()
  } catch (error) {
    console.error('Error fetching community data:', error)
  }
})
</script>
<template>
  <div class="community">
    <div class="subtitle | js-community">
      <h1>Connect with other travelers in our community</h1>
    </div>
    <div class="cards-com">
      <swiper-container
        :slides-per-view="'auto'"
        :loop="true"
        :space-between="20"
        direction="horizontal"
      >
        <swiper-slide v-for="(item, index) in community" :key="index" class="swiper-slide">
          <CommunityItem
            :community-id="item.id"
            :title="item.title"
            :description="item.description"
            :image="item.image"
          />
        </swiper-slide>
      </swiper-container>
    </div>
  </div>
</template>
<style>
.community h1 {
  color: black;
  margin-left: 10%;
}
.cards-com {
  margin-left: 10%;
}

.card-com {
  border-radius: 18px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  flex: 0 0 auto;
  width: 380px;
  margin-bottom: 5%;
  padding-top: 5%;
}

.card-com-image {
  width: 90%;
  height: auto;
  display: block;
  border-radius: 18px;
  margin-left: 5%;
}

.card-com-content {
  margin-left: 5%;
  padding-bottom: 5%;
}

.card-com-title {
  font-size: 1.5em;
  color: #333;
}

.card-com-description {
  font-size: 1em;
  color: #555;
}

@media (max-width: 1200px) {
  .card-com {
    width: 230px;
  }
}
</style>
