<script setup>
import { ref, onMounted } from 'vue'
import HeroSkeleton from './TheWelcomeSkeleton.vue'
import flatpickr from 'flatpickr'
import 'flatpickr/dist/flatpickr.min.css'

document.addEventListener('DOMContentLoaded', function () {
  flatpickr('.date-picker', {})
})

const isLoading = ref(true)
const backgroundImage = ref(null)
const searchImage = ref(null)
const checksImage = ref(null)
const personsImage = ref(null)

const apiPageUrl = `${import.meta.env.VITE_API_PAGE_URL}`

onMounted(async () => {
  try {
    const response = await fetch(apiPageUrl)
    if (!response.ok) throw new Error('Failed to fetch images')

    const data = await response.json()
    backgroundImage.value = data?.background_image || null
    searchImage.value = data?.search_image || null
    checksImage.value = data?.checks_image || null
    personsImage.value = data?.persons_image || null
  } catch (error) {
    console.error('Error fetching images:', error)
  } finally {
    isLoading.value = false
  }
})
</script>

<template>
  <section v-if="isLoading">
    <HeroSkeleton />
  </section>
  <section v-else class="hero">
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

<style>
.hero {
  position: relative;
  overflow: hidden;
}

.hero-bg {
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  color: white;
  min-height: 100vh;
}

.hero-bg::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(180deg, rgba(255, 255, 255, 0) 90%, #ffffff 100%);
  pointer-events: none;
}

.container {
  margin-left: 10%;
  margin-right: 10%;
}

.title {
  font-size: 80px;
  font-weight: 700;
  padding-top: 7%;
}

.title h1 {
  margin: 0;
  padding: 0;
}

.search-bar input::placeholder {
  color: white;
}

.search-bar {
  display: flex;
  align-items: center;
  background-color: rgba(255, 255, 255, 0.4);
  backdrop-filter: blur(35.424930572509766px);
  border-radius: 17px;
  padding: 15px;
}

.search-bar input {
  flex: 1;
  border: 0;
  background-color: transparent;
  box-sizing: border-box;
  padding: 13.28px 8.86px 13.28px 8.86px;
  color: white;
}

.search-bar select {
  border: 0;
  background-color: transparent;
  box-sizing: border-box;
  padding: 13.28px 8.86px 13.28px 8.86px;
  color: white;
}

.search-bar button {
  padding: 13.28px 35.42px 13.28px 35.42px;
  margin-right: 20px;
  background-color: rgba(255, 255, 255, 1);
  color: rgba(38, 89, 195, 1);
  border: none;
  border-radius: 35px;
  cursor: pointer;
  display: inline-block;
}

.search {
  background-repeat: no-repeat;
  background-position: 10px center;
  width: 100%;
  position: relative;
}

.search input {
  padding-left: 40px;
  width: 100%;
  border: none;
  outline: none;
  transition: border-color 0.3s ease-in-out;
}

.search label {
  position: absolute;
  left: 50px;
  top: 50%;
  transform: translateY(-50%);
  color: white;
  font-size: 16px;
  transition: all 0.3s ease-in-out;
  pointer-events: none;
}

.search input:focus + label,
.search input:not(:placeholder-shown) + label {
  top: 7px;
  font-size: 10px;
  color: black;
}

.check-cal {
  background-repeat: no-repeat;
  background-position: 10px center;
}

.check-cal input {
  padding-left: 40px;
  border: none;
  outline: none;
  width: 100%;
}

.checks {
  display: flex;
}

.persons-icon {
  flex: 1;
  background-repeat: no-repeat;
  background-position: 10px center;
}

.persons-icon select {
  padding-left: 40px;
  border: none;
  outline: none;
  appearance: none;
}

.hero-subtitle {
  color: white;
}

@media (max-width: 1200px) {
  .title {
    padding-top: 20%;
    font-size: 32px;
  }
  .hero-bg {
    min-height: 50vh !important;
  }

  .hero-subtitle {
    color: black;
  }

  .search-bar {
    flex-direction: column;
    align-items: flex-start;
    background-color: transparent;
    backdrop-filter: none;
  }

  .search-bar label,
  .search-bar input,
  .search-bar select {
    font-weight: 200;
  }

  .search-bar .search {
    width: 100%;
    margin-bottom: 10px;
    background-color: rgba(255, 255, 255, 0.4);
    backdrop-filter: blur(35.424930572509766px);
    border-radius: 35px;
    padding-right: 0;
    box-sizing: border-box;
  }

  .search input {
    width: 100%;
    padding: 15px;
    padding-left: 35px;
  }

  .check-cal input {
    width: 100%;
  }

  .search-bar .checks {
    width: 100%;
    margin-bottom: 10px;
    background-color: rgba(255, 255, 255, 0.4);
    backdrop-filter: blur(35.424930572509766px);
    border-radius: 35px;
    padding-right: 0;
    box-sizing: border-box;
  }

  .checks input {
    padding: 15px;
    padding-left: 40px;
  }

  .search-bar .persons-icon {
    width: 100%;
    margin-bottom: 10px;
    background-color: rgba(255, 255, 255, 0.4);
    backdrop-filter: blur(35.424930572509766px);
    border-radius: 35px;
    padding-right: 0;
    box-sizing: border-box;
    padding: 9px;
  }

  .search-bar button {
    width: 100%;
    margin-right: 0;
    background-color: rgba(38, 89, 195, 1);
    color: white;
  }
  .search-bar button {
    margin-bottom: 10%;
  }
}

.subtitle h1 {
  font-size: 36px;
  font-weight: 700;
  margin-bottom: 20px;
}
</style>
