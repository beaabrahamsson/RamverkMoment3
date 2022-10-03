<script>
import { RouterView } from 'vue-router'
import Header from "./components/Header.vue";
import HeroImage from './components/HeroImage.vue';
import Footer from './components/Footer.vue';

export default {
  components: {
    Header,
    RouterView,
    HeroImage,
    Footer
}
}
</script>

<template>
  <HeroImage />
  <Header />
  <main>
    <RouterView />
  </main>
  <Footer />
</template>

<style scoped>
  main {
    max-width: 1000px;
    width: 100%;
    margin: 0 auto;
  }
</style>
