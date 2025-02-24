<script setup>
import { ref, onMounted } from 'vue'

const footerData = ref(null)

onMounted(async () => {
  try {
    const response = await fetch('http://localhost/trxvl/wp-json/trxvl/v1/footer')
    if (!response.ok) throw new Error('Failed to fetch footer data')

    footerData.value = await response.json()
  } catch (error) {
    console.error('Error fetching footer data:', error)
  }
})
</script>

<template>
  <footer v-if="footerData">
    <div class="container">
      <div class="footer">
        <div class="footer-left">
          <div class="logo">
            <h1>{{ footerData.footer_logo }}</h1>
          </div>
        </div>
        <div class="footer-menus">
          <div
            class="footer-menu"
            v-for="(menuGroup, index) in footerData.footer_menus"
            :key="index"
          >
            <ul>
              <li v-for="(menu, i) in menuGroup.menu_items" :key="i">
                <a :href="menu.menu_item_link">{{ menu.menu_item_text }}</a>
              </li>
            </ul>
          </div>
        </div>
      </div>
      <div class="footer-down">
        <div class="footer-btn">
          <button>{{ footerData.button_text }}</button>
        </div>
        <div class="footer-social">
          <a
            v-for="(social, index) in footerData.footer_social"
            :key="index"
            :href="social.social_link"
          >
            <img v-if="social.social_image_url" :src="social.social_image_url" alt="Social Icon" />
          </a>
        </div>
      </div>

      <div class="footer-copyright">
        <p>© 1997-2021 Netflix, Inc. {i-062d573a0ee099242}</p>
      </div>
    </div>
  </footer>
</template>
<style>
footer h1 {
  margin: 0;
}
footer {
  color: white;
  background: rgba(20, 20, 20, 1);
}

.footer {
  display: flex;
  flex-direction: row;
  padding-top: 50px;
}

.footer-logo {
  font-size: 35.42px;
  font-weight: 700;
}

.footer-menus {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  margin-left: 10%;
}

.footer-menus ul {
  list-style-type: none;
}

.footer-menu li {
  padding-bottom: 15px;
}

.footer-menus a {
  text-decoration: none;
  color: rgba(128, 128, 128, 1);
  font-size: 14.39px;
  font-weight: 400;
}

.footer-down {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-between;
  margin-left: 20%;
}

.footer-social a {
  padding-right: 22.14px;
}

.footer-btn button {
  padding: 11.07px 16.61px 11.07px 16.61px;
  gap: 0px;
  border: 1.11px solid rgba(128, 128, 128, 1);
  background-color: transparent;
  color: rgba(128, 128, 128, 1);
  opacity: 0px;
}

.footer-copyright {
  color: rgba(128, 128, 128, 1);
  margin-top: 2%;
  padding-bottom: 5%;
}

.footer-copyright p {
  margin: 0;
  text-align: center;
}

@media (max-width: 1200px) {
  .footer-btn {
    padding-bottom: 30px;
  }
  .footer-social {
    padding-bottom: 10px;
  }
  .footer-copyright p {
    margin: 0;
    margin-bottom: 30%;
  }
}
</style>
