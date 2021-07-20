<template>
  <div class="message-container">
    <p>{{ msg }}</p>
  </div>
</template>

<script>

export default ({
  props: {
    msg: String
  },
  date() {
    return {

    }
  }
})
</script>

<style scoped>
  .message-container {
    text-align: center;
    color: #fff;
    background-color: #FCBA03;
    border: 1px solid #FCBA03;
    border-radius: .1rem;
    padding: 10px;
    max-width: 450px;
    margin: 30px auto;
  }
</style>