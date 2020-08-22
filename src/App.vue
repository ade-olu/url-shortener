<template>
<!-- Created By Oluwatobiloba Adegbaju -->
  <div id="app">
    <page-nav></page-nav>
   <url-shortener></url-shortener>
   <page-footer></page-footer>
  </div>
</template>

<script>
import UrlShortener from './components/UrlShortener.vue'
import Nav from './components/Nav.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App'
  components: {
    'url-shortener': UrlShortener,
    'page-nav': Nav,
    'page-footer': Footer
  }
}
</script>

<style lang="scss">
* {
  margin: 0 !important;
  padding: 0 !important;
}
</style>
