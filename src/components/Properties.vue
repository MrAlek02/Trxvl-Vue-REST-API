<script setup>
import { ref, onMounted } from 'vue'
import PropertyItem from './PropertyItem.vue'

import { register } from 'swiper/element/bundle'
register()

const properties = ref([])

onMounted(async () => {
  try {
    const response = await fetch(`http://localhost/trxvl/wp-json/trxvl/v1/properties`)
    if (!response.ok) throw new Error('Failed to fetch properties')

    properties.value = await response.json()
  } catch (error) {
    console.error('Error fetching properties:', error)
  }
})
</script>

<template>
  <div class="property">
    <div class="container">
      <div class="subtitle | js-property">
        <h1>Browse by property type</h1>
      </div>
    </div>
    <div class="destinations">
      <swiper-container
        :slides-per-view="'auto'"
        :loop="true"
        :space-between="20"
        direction="horizontal"
      >
        <swiper-slide class="swiper-slide" v-for="property in properties" :key="property.id">
          <PropertyItem :property="property" />
        </swiper-slide>
      </swiper-container>
    </div>
  </div>
</template>
