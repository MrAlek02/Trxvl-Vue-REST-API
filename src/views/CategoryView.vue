<script setup>
import { ref, onMounted, computed, watch } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import Header from '@/components/Header.vue'
import Hero from '@/components/CategoryTemplate/Hero.vue'
import Categories from '@/components/Categories.vue'
import Destinations from '@/components/CategoryTemplate/Destinations.vue'
import Recently from '@/components/CategoryTemplate/Recently.vue'
import Inclusive from '@/components/CategoryTemplate/Inclusive.vue'
import Honeymoon from '@/components/CategoryTemplate/Honeymoon.vue'
import Footer from '@/components/Footer.vue'

const categories = ref([])
const excludedCategoryId = 1

const route = useRoute()
const router = useRouter()

const selectedSlug = computed(() => route.params.slug || null)

let matchedId = ref(null)

const fetchCategories = async () => {
  try {
    const response = await fetch(
      `http://localhost/trxvl/wp-json/wp/v2/categories?exclude=${excludedCategoryId}`,
    )
    if (!response.ok) throw new Error('Failed to fetch categories')

    categories.value = await response.json()

    if (selectedSlug.value) {
      const matchedCategory = categories.value.find(
        (category) => category.slug === selectedSlug.value,
      )
      matchedId.value = matchedCategory ? matchedCategory.id : null
      console.log(matchedId.value)
    }
  } catch (error) {
    console.error('Error fetching categories:', error)
  }
}

const selectSlug = (slug) => {
  router.push({ params: { slug } })
}

// Watch for changes to selectedSlug and refetch categories when it changes
watch(
  selectedSlug,
  () => {
    fetchCategories()
  },
  { immediate: true },
)

onMounted(() => {
  fetchCategories()
})
</script>

<template>
  <div v-if="matchedId !== null">
    <Header />
    <Hero :categoryId="matchedId" />
    <Categories :categories="categories" @category-click="selectSlug" />
    <Destinations :categoryId="matchedId" />
    <Recently :categoryId="matchedId" />
    <Inclusive :categoryId="matchedId" />
    <Honeymoon :categoryId="matchedId" />
    <Footer />
  </div>

  <div v-else>Loading...</div>
</template>
