<script setup>
import { useRoute } from 'vue-router'
import Hero from '@/components/Mountains/Hero.vue'
import Categories from '@/components/Categories.vue'
import Destinations from '@/components/Mountains/Destinations.vue'
import Recently from '@/components/Mountains/Recently.vue'
import Inclusive from '@/components/Mountains/Inclusive.vue'
import Honeymoon from '@/components/Mountains/Honeymoon.vue'
import Footer from '@/components/Footer.vue'

const route = useRoute()
const category = route.params.category
</script>

<template>
  <Hero :category="category" />
  <Categories :category="category" />
  <Destinations :category="category" />
  <Recently :category="category" />
  <Inclusive :category="category" />
  <Honeymoon :category="category" />
  <Footer />
</template>
