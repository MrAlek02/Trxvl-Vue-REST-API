<script setup>
import { defineProps, ref, onMounted } from 'vue'

const props = defineProps({
  id: {
    type: Number,
  },
  title: {
    type: String,
  },
  url: {
    type: String,
  },
  excerpt: {
    type: String,
  },
  thumbnail: {
    type: String,
  },
  rating: {
    type: String,
  },
  star: {
    type: String,
  },
  stays: {
    type: String,
  },
  flights_text: {
    type: String,
  },
  flights: {
    type: String,
  },
  hotels_text: {
    type: String,
  },
  hotels: {
    type: String,
  },
  transfers_text: {
    type: String,
  },
  transfers: {
    type: String,
  },
  activities_text: {
    type: String,
  },
  activities: {
    type: String,
  },
  list: {
    type: String,
  },
  price_text: {
    type: String,
  },
  price_sale_text: {
    type: String,
  },
  per: {
    type: String,
  },
})

const isLoading = ref(true)

onMounted(() => {
  setTimeout(() => {
    isLoading.value = false
  }, 3000)
})
</script>

<template>
  <div v-if="isLoading">
    <div class="skeleton-box skeleton-image"></div>
  </div>

  <div v-else class="card-mtn | js-recently">
    <a href="#">
      <img class="thumbnail" :src="thumbnail" :alt="title" />
      <div class="card-mtn-content">
        <div class="mtn-title-row">
          <h2>{{ title }}</h2>
          <img :src="star" />
          <h2>{{ rating }}</h2>
        </div>
        <h3>{{ stays }}</h3>
        <div class="mtn-icons">
          <div class="mtn-icon">
            <img :src="flights" />
            <p>{{ flights_text }}</p>
          </div>
          <div class="mtn-icon">
            <img :src="hotels" />
            <p>{{ hotels_text }}</p>
          </div>
          <div class="mtn-icon">
            <img :src="transfers" />
            <p>{{ transfers_text }}</p>
          </div>
          <div class="mtn-icon">
            <img :src="activities" />
            <p>{{ activities_text }}</p>
          </div>
        </div>
        <ul v-html="list"></ul>
        <div class="mtn-price">
          <h3>{{ price_sale_text }}</h3>
          <h2>{{ price_text }}</h2>
          <p>{{ per }}</p>
        </div>
      </div>
    </a>
  </div>
</template>

<style scoped>
.skeleton-image {
  width: 350px;
  height: 200px;
}

.skeleton-box {
  background: #e0e0e0;
  border-radius: 8px;
  animation: pulse 1.5s infinite ease-in-out;
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
