<script setup>
import { ref, onMounted } from 'vue'

const backgroundImage = ref(null)
const appTitle = ref(null)
const appDescription = ref(null)
const appText = ref(null)
const appImage = ref(null)
const buttonMobile = ref(null)
const buttonEmail = ref(null)
const searchText = ref(null)
const searchButton = ref(null)
const appStore = ref(null)
const googleStore = ref(null)

const appSectionUrl = import.meta.env.VITE_API_APP_SECTION_URL

onMounted(async () => {
  try {
    const response = await fetch(appSectionUrl)
    if (!response.ok) throw new Error('Failed to fetch posts')

    const data = await response.json()

    backgroundImage.value = data?.background_image || null
    appTitle.value = data?.app_title || null
    appDescription.value = data?.app_description || null
    appText.value = data?.app_text || null
    appImage.value = data?.app_image || null
    buttonMobile.value = data?.button_mobile || null
    buttonEmail.value = data?.button_email || null
    searchText.value = data?.search_text || null
    searchButton.value = data?.button_search || null
    appStore.value = data?.app_store || null
    googleStore.value = data?.google_store || null
  } catch (error) {
    console.error('Error fetching posts:', error)
  }
})
</script>
<template>
  <div class="app | js-app">
    <div
      class="app-bg"
      :style="{ backgroundImage: backgroundImage ? `url(${backgroundImage})` : 'none' }"
    >
      <div class="app-container">
        <div class="app-mockup | js-mobile">
          <img :src="appImage" alt="App Mockup" />
        </div>
        <div class="app-content | js-content">
          <h1>{{ appTitle }}</h1>
          <h2>{{ appDescription }}</h2>
          <div class="app-inputs">
            <div class="app-input | js-content">
              <button class="active">{{ buttonMobile }}</button>
              <button>{{ buttonEmail }}</button>
              <p>{{ appText }}</p>
              <div class="app-src-input | js-content">
                <input type="text" :placeholder="searchText" />
                <button class="app-src-btn">{{ searchButton }}</button>
              </div>
            </div>
            <div class="app-input | js-content">
              <svg
                width="2"
                height="57"
                viewBox="0 0 2 57"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <line
                  opacity="0.2"
                  x1="0.641649"
                  y1="0.144043"
                  x2="0.641647"
                  y2="56.9825"
                  stroke="white"
                  stroke-width="1.10703"
                />
              </svg>
              <p>or</p>
              <svg
                width="2"
                height="57"
                viewBox="0 0 2 57"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <line
                  opacity="0.2"
                  x1="0.641649"
                  y1="0.144043"
                  x2="0.641647"
                  y2="56.9825"
                  stroke="white"
                  stroke-width="1.10703"
                />
              </svg>
            </div>
            <div class="app-input | js-content">
              <img :src="googleStore" alt="Google Store" />
              <img :src="appStore" alt="App Store" />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style>
.app {
  margin-top: 10%;
}

.app-bg {
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  height: 70vh;
  position: relative;
}

.app-container {
  margin-top: auto;
  display: flex;
  flex-direction: row;
  margin-left: 10%;
  margin-right: 10%;
  position: absolute;
  bottom: 0;
  color: white;
}

.app-content {
  margin-left: 50px;
}

.app-content h1 {
  font-size: 53px;
  font-weight: 700;
}

.app-content h2 {
  font-size: 26.57px;
  font-weight: 400;
}

.app-inputs button {
  background-color: transparent;
  border: 0;
  color: white;
  padding: 8.86px 17.71px 8.86px 17.71px;
  border-radius: 18px;
}

.app-inputs button.active {
  background: rgba(255, 255, 255, 0.4);
  backdrop-filter: blur(35.424930572509766px);
}

.app-src-input {
  display: flex;
  background: rgba(255, 255, 255, 0.4);
  backdrop-filter: blur(35.424930572509766px);
  border-radius: 18px;
  padding: 8.86px 17.71px 8.86px 17.71px;
}

.app-src-input input {
  background-color: transparent;
  border: 0;
  border-radius: 18px;
  padding: 13.28px 8.86px 13.28px 8.86px;
  flex: 1;
}

.app-src-input input:focus {
  outline: none;
}

.app-src-input button {
  background: rgba(255, 255, 255, 1);
  border-radius: 35.42px;
  padding: 13.28px 35.42px 13.28px 35.42px;
  color: rgba(38, 89, 195, 1);
}

.app-inputs {
  display: flex;
  flex-direction: row;
  gap: 100px;
}

@media (max-width: 1200px) {
  .app-container {
    flex-direction: column-reverse;
    /* flex-direction: column; */
    align-items: center;
    text-align: center;
    position: relative;
  }

  .app-inputs {
    flex-direction: column;
    align-items: center;
  }

  .app-bg {
    height: auto;
  }

  .app-content {
    margin-left: 0;
  }

  .app-content h1 {
    font-size: 36px;
  }

  .app-content h2 {
    font-size: 18px;
  }

  .app-src-input {
    flex-direction: column;
    align-items: center;
  }

  .app-src-input input {
    width: 100%;
    text-align: center;
  }

  .app-src-input button {
    width: 100%;
    margin-top: 10px;
  }
  .app-mockup {
    padding-top: 5%;
  }
}
</style>
