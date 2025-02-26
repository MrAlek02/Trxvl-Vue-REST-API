<script setup>
import { ref, onMounted } from 'vue'
import DestinationsItem from './Items.vue'

import { register } from 'swiper/element/bundle'
register()

const posts = ref([])

onMounted(async () => {
  try {
    const response = await fetch('http://localhost/trxvl/wp-json/trxvl/v1/categories/post/22')
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
        <DestinationsItem
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
<style>
.swiper-slide {
  width: fit-content !important;
}

.destinations-mtn {
  margin-left: 10%;
  margin-bottom: 5%;
}

.destination-mtn {
  position: relative;
  top: 10;
}

.card-mtn {
  display: flex;
  flex-direction: column;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
  border-radius: 17px;
  background-color: white;
  height: auto;
  width: auto;
  padding: 16px;
  margin-bottom: 5%;
}

.card-mtn img {
  border-radius: 8px;
}

.card-mtn a {
  text-decoration: none;
  color: black;
}

.card-mtn h2 {
  font-weight: 400;
}

.card-mtn h3 {
  font-weight: 400;
  opacity: 50%;
  padding: 0;
  margin: 0;
}

.mtn-title-row {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}

.mtn-title-row img {
  margin-left: auto;
  margin-right: 5px;
}

.mtn-icons {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  margin-top: 10%;
}

.mtn-icon {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.mtn-icon p {
  margin: 0;
  padding: 0;
  opacity: 50%;
  font-weight: 400;
  padding-top: 10px;
}

.card-mtn ul {
  padding-left: 16px;
}

.card-mtn li {
  padding: 5px;
  opacity: 50%;
}

.mtn-price {
  display: flex;
  flex-direction: row;
}

.mtn-price h3 {
  text-decoration: line-through;
  opacity: 50%;
  font-weight: 100;
}

.mtn-price h2 {
  font-weight: 700;
  margin: 0;
  margin-left: 10%;
}

.mtn-price p {
  opacity: 50%;
  font-weight: 400;
  margin: 0;
  font-size: 13px;
  margin-top: 10px;
}
</style>
