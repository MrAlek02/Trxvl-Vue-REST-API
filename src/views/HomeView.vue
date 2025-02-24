<script setup>
import TheWelcome from '../components/TheWelcome.vue'
import Header from '../components/Header.vue'
import Categories from '../components/Categories.vue'
import Destinations from '../components/Destinations.vue'
import Offers from '../components/Offers.vue'
import Properties from '../components/Properties.vue'
import PageImage from '../components/PageImage.vue'
import Community from '../components/Community.vue'
import AppSection from '../components/AppSection.vue'
import Footer from '../components/Footer.vue'
</script>

<template>
  <Header />
  <main>
    <TheWelcome />
    <Categories />
    <Destinations />
    <Offers />
    <Properties />
    <PageImage />
    <Community />
    <AppSection />
    <Footer />
  </main>
</template>
