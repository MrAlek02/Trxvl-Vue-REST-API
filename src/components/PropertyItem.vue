<script setup>
import { defineProps } from 'vue'

const props = defineProps({
  property: Object,
})
</script>

<template>
  <div v-if="property" class="destination | js-property">
    <img v-if="property.image" :src="property.image" :alt="property.name" />
    <div class="destination-info">
      <h2>{{ property.name }}</h2>
    </div>
  </div>
</template>
