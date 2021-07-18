<template>
  <div id="nav">
    <router-link to="/" id="logo-url" class="logo"> 
      <img :src="logo" :alt="alt" id="logo">
      <h2>Well Burgers</h2>
    </router-link>

    <router-link to="/">Home</router-link>
    <router-link to="/pedidos">Pedidos</router-link>
  </div>
</template>

<script>
  export default ({
    name: 'Navbar',
    props: ['logo', 'alt'],

    data() {
      return {

      }
    },
  })
</script>

<style scoped>
  #nav {
    background-color: #222;
    border-bottom: 4px solid #111;
    padding: 15px 50px;

    display: flex;
    justify-content: flex-end;
    align-items: center;
  }

  #nav #logo-url {
    margin:  auto;
    margin-left: 0;

    display: flex;
    align-items: center;
  }

  #logo {
    width: 40px;
    height: 40px;
  }

  #nav #logo-url h2 {
    font-weight: 100;
    font-size: 34px;
    margin-left: .5rem;
  }

  #nav a {
    color: #FCBA03;
    text-decoration: none;
    margin: 12px;
    transition: .5s;
  }

  #nav a:hover {
    color: #FFF;
  }
</style>
