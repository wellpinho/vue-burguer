<template>
  <Navbar :logo="logoSrc" :alt="altName" />
  <router-view />
  <Footer />
</template>

<script>
import Navbar from './components/Navbar.vue';
import Footer from './components/Footer.vue'

export default ({
  components: {
    Navbar,
    Footer
  },
  data() {
    return {
      logoSrc: '/img/logo.png',
      altName: 'Make your burguer'
    }
  },
})
</script>


<style>

  *, html {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Arial, Helvetica, sans-serif;
  }

  .main-container {
    margin: 50px;
    min-height: 250px;
  }

  h1 {
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: #222;
  }

</style>
