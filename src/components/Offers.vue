<script setup>
import { ref, onMounted } from 'vue'
import OfferItem from './OfferItem.vue'
import { register } from 'swiper/element/bundle'

register()

const offers = ref([])

const apiOffersUrl = `${import.meta.env.VITE_API_OFFERS_URL}`

onMounted(async () => {
  try {
    const response = await fetch(apiOffersUrl)
    if (!response.ok) throw new Error('Failed to fetch posts')

    offers.value = await response.json()
  } catch (error) {
    console.error('Error fetching posts:', error)
  }
})
</script>

<template>
  <div class="about">
    <div class="subtitle | js-about">
      <h1>Offers</h1>
    </div>
    <swiper-container
      :slides-per-view="'auto'"
      :loop="true"
      :space-between="20"
      direction="horizontal"
    >
      <swiper-slide class="swiper-slide" v-for="offer in offers" :key="offer.id">
        <OfferItem
          :offer-id="offer.id"
          :title="offer.title"
          :subtitle="offer.subtitle"
          :description="offer.description"
          :textbutton="offer.textbutton"
          :image="offer.image"
        />
      </swiper-slide>
    </swiper-container>
  </div>
</template>
<style>
.about {
  margin-left: 10%;
  color: black;
}

.card {
  display: flex;
  align-items: center;
  background-color: #fff;
  border-radius: 17px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  width: 760px;
  height: 290px;
  margin: 16px;
}

.card-image {
  border-radius: 23px;
  margin-left: 10px;
  margin-top: 20px;
  margin-bottom: 20px;
}

.card-content {
  padding: 16px 24px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.card-subtitle {
  font-size: 17px;
  opacity: 0.5;
  font-weight: 400;
  margin: 0;
}

.card-title {
  font-size: 27px;
  font-weight: 500;
  color: #333;
  margin: 15px 0;
}

.card-description {
  font-size: 17px;
  opacity: 0.5;
  margin: 15px 0;
}

.card-button {
  margin-top: 15px;
  padding: 17.71px 35.42px 17.71px 35.42px;
  width: 154px;
  color: #fff;
  font-size: 17px;
  font-weight: 400;
  background-color: rgba(38, 89, 195, 1);
  border: none;
  border-radius: 35px;
  cursor: pointer;
}

.card-button:hover {
  opacity: 0.5;
}

.property {
  color: black;
}

@media (max-width: 1200px) {
  .card {
    display: flex;
    flex-direction: column;
    width: 300px;
    height: auto;
  }

  .card-image {
    margin-left: 0;
  }

  .card img {
    width: 250px;
  }
}
</style>
