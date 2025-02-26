<script setup>
import { ref, onMounted } from 'vue'
import CategoryItem from './CategoryItem.vue'

import { register } from 'swiper/element/bundle'
register()

const categories = ref([])
const excludedCategoryId = 1

onMounted(async () => {
  try {
    const response = await fetch(
      `http://localhost/trxvl/wp-json/wp/v2/categories?exclude=${excludedCategoryId}`,
    )
    if (!response.ok) throw new Error('Failed to fetch categories')

    categories.value = await response.json()
  } catch (error) {
    console.error('Error fetching categories:', error)
  }
})
</script>

<template>
  <div class="categories-margin">
    <div class="container">
      <div class="hero-subtitle | js-categories">
        <h1>Top categories</h1>
      </div>
    </div>
    <div class="categories">
      <swiper-container
        :slides-per-view="'auto'"
        :loop="true"
        :space-between="20"
        direction="horizontal"
      >
        <swiper-slide class="swiper-slide" v-for="category in categories" :key="category.id">
          <router-link :to="`/categories/${category.slug}`">
            <CategoryItem :categoryId="category.id" />
          </router-link>
        </swiper-slide>
      </swiper-container>
    </div>
  </div>
</template>
<style>
.swiper-slide {
  width: fit-content !important;
}

.hero-subtitle {
  color: white;
  position: relative;
  top: 20;
  margin-bottom: 20px;
}

.categories {
  margin-left: 10%;
  margin-right: 10%;
}

.categories h1 {
  color: white;
  opacity: 50%;
  text-decoration: none;
  font-size: 15px;
}

.categories h1:hover {
  color: white;
  opacity: 100%;
  text-decoration: none;
}

.categories-margin {
  margin-top: -20%;
}

.category {
  display: flex;
  align-items: center;
  justify-content: center;
  display: block;
  margin-right: 75px;
}

.category img {
  margin-left: auto;
  margin-right: auto;
  display: block;
  opacity: 50%;
}

@media (max-width: 1200px) {
  .categories {
    filter: drop-shadow(0 0 black);
    margin-right: 0;
  }
  .categories-margin {
    margin-top: 0;
  }
  .category {
    margin-right: 0 !important;
  }
  .category h1:hover {
    color: black;
  }
  .destination img {
    width: 230px;
  }
  .subtitle h1 {
    font-size: 24px;
  }
  .hero-subtitle h1 {
    font-size: 24px;
    color: black;
  }
}
</style>
