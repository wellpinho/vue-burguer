<template>
  <footer id="footer">
    <p>Make Your Burger &copy; - Since {{ year }}</p>
  </footer>
</template>

<script>
  const year = new Date().getFullYear();

  export default ({
    name: 'Footer',

    data() {
      return {
        year
      }
    }
  })
</script>

<style scoped>
  #footer {
    height: 200px;
    background-color: #222;
    border-top: 4px solid #111;
    color: #FCBA03;

    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
