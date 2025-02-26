<script setup>
import { ref, onMounted } from 'vue'

const backgroundImage = ref(null)
const searchImage = ref(null)
const checksImage = ref(null)
const personsImage = ref(null)

onMounted(async () => {
  try {
    const response = await fetch('http://localhost/trxvl/wp-json/trxvl/v1/categories/22')
    if (!response.ok) throw new Error('Failed to fetch images')

    const data = await response.json()
    backgroundImage.value = data?.hero_background || null
    searchImage.value = data?.search_image || null
    checksImage.value = data?.checks_image || null
    personsImage.value = data?.person_image || null
  } catch (error) {
    console.error('Error fetching images:', error)
  } finally {
    isLoading.value = false
  }
})
</script>
<template>
  <section class="hero">
    <div
      class="hero-bg"
      :style="{ backgroundImage: backgroundImage ? `url(${backgroundImage})` : 'none' }"
    >
      <div class="container">
        <div class="title">
          <h1>The whole world <br />awaits.</h1>
        </div>
        <div class="search-bar">
          <div
            class="search"
            :style="{ backgroundImage: searchImage ? `url(${searchImage})` : 'none' }"
          >
            <input class="search-input" id="input-field" type="search" placeholder="" required />
            <label for="input-field">Search destinations, hotels</label>
          </div>
          <div class="checks">
            <div
              class="check-cal"
              :style="{ backgroundImage: checksImage ? `url(${checksImage})` : 'none' }"
            >
              <input
                class="checkIn date-picker"
                id="dateInput"
                type="text"
                placeholder="Check in"
              />
            </div>
            <div
              class="check-cal"
              :style="{ backgroundImage: checksImage ? `url(${checksImage})` : 'none' }"
            >
              <input
                class="checkOut date-picker"
                id="dateInputSecond"
                type="text"
                placeholder="Check out"
              />
            </div>
          </div>
          <div
            class="persons-icon"
            :style="{ backgroundImage: personsImage ? `url(${personsImage})` : 'none' }"
          >
            <select name="persons" class="persons">
              <option value="1room">1 room, 2 adults</option>
              <option value="1room2">1 room, 1 adult</option>
              <option value="2room2">2 rooms, 2 adults</option>
              <option value="2room3">2 room, 3 adults</option>
            </select>
          </div>
          <button type="submit">Search</button>
        </div>
      </div>
    </div>
  </section>
</template>
