<template>
  <div id="main-banner">
    <h1>Make your burger</h1>
  </div>
</template>

<script>

export default ({
  name: 'Banner',

  data() {
    return {

    }
  },
})
</script>

<style scoped>
  #main-banner {
    background-image: url('/img/burger.jpg');
    background-position: 0 center;
    background-repeat: no-repeat;
    background-size: cover;
    padding: 0 15px;
    height: 600px;

    display: flex;
    justify-content: flex-start;
    align-items: center;
  }

  #main-banner h1 {
    color: #FFF;
    text-align: center;
    font-size: 60px;
    background-color: rgba(34, 34, 34, 0.582);
    padding: 20px 40px;
  }
</style>