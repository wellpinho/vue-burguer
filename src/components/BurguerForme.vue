<template>
  <div>
    <p>Componente de mensagem</p>
    <div>
      <form id="burger-form">
        <div class="input-container">
          <label for="name">Nome do Cliente</label>
          <input 
            type="text" 
            id="name" 
            v-model="name" 
            name="name" 
            placeholder="Digite seu nome..."
          >
        </div>

        <div class="input-container">
          <label for="bread">Escolha o pão</label>
          <select 
            name="bread" 
            id="bread" 
            v-model="bread"
          >
            <option 
              v-for="bread in breads" 
              :key="bread.id" 
              :value="bread.tipo"
            >
              {{ bread.tipo }}
            </option>
          </select>
        </div>

        <div class="input-container">
          <label for="beef">Escolha a carne</label>
          <select 
            name="beef" 
            id="beef" 
            v-model="bread"
          >
            <option 
              v-for="beef in beefs" 
              :value="beef.tipo"
              :key="beef.id"
            >
              {{ beef.tipo }}
            </option>
          </select>
        </div>

        <div id="opcionals-container " class="input-container">
          <label id="optionals-title" for="optionals">Escolha os opcionais:</label>
          <div 
            class="checkbox-container"
            v-for="optional in optionalsArr"
            :key="optional.id"
          >
            <input 
              type="checkbox" 
              name="optionals" 
              v-model="optionals" 
              :value="optional.tipo"
            >
            <span>{{ optional.tipo }}</span>
          </div>

          <div class="input-container">
            <input 
              type="submit" 
              class="submit-btn" 
              value="Criar meu Burger!"
            >
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>

export default ({
  name: 'FormBurger',

  data() {
    return {
      breads: null,
      beefs: null,
      optionalsArr: null,
      name: null,
      beef: null,
      optional: [],
      status: "Solicitado",
      msg: null
    }
  },
  methods: {
    async getIngredients() {
      const req = await fetch('http://localhost:3000/ingredientes');
      const data = await req.json();

      this.breads = data.paes;
      this.beefs = data.carnes;
      this.optionalsArr = data.opcionais;
    }
  },
  mounted() {
    this.getIngredients()
  }
})
</script>

<style scoped>
  #burger-form {
    max-width: 400px;
    margin: 0 auto; 
  }

  .input-container {
    margin-bottom: 20px;

    display: flex;
    flex-direction: column;
  }

  label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;
    padding: 5px 10px;
    border-left: 4px solid #FCBA03;
  }

  input, select {
    padding: 5px 10px;
    width: 300px;
  }

  #opcionals-container {
    flex-direction: row;
    flex-wrap: wrap;
  }

  #optionals-title {
    width: 100%;
  }

  .checkbox-container {
    width: 50%;
    margin-bottom: 20px;

    display: flex;
    align-items: flex-start;
  }

  .checkbox-container span,
  .checkbox-container input {
    width: auto;
  }

  .checkbox-container span {
    margin-left: 6px;
    font-weight: bold;
  }

  .submit-btn {
    background-color: #222;
    color: #FCBA03;
    font-weight: bold;
    border: 1px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0;
    cursor: pointer;
    transition: .5s;
    border-radius: .2rem;
  }

  .submit-btn:hover {
    background-color: #FCBA03;
    color: #222;
  }
</style>