<template>
  <div>
    <Message :msg="msg" v-show="msg" />
    <div>
      <form id="burger-form" @submit.prevent="createBurger">
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
            v-model="beef"
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
import Message from './../components/Msg.vue';

export default ({
  name: 'FormBurger',
  components: {
    Message
  },
  data() {
    return {
      breads: null,
      beefs: null,
      optionalsArr: null,
      name: null,
      bread: 'Integral',
      beef: 'Picanha',
      optionals: [],
      status: "Solicitado",
      msg: null
    }
  },
  methods: {
    async getIngredients() {
      const request = await fetch('http://localhost:3000/ingredientes');
      const data = await request.json();

      this.breads = data.breads;
      this.beefs = data.beefs;
      this.optionalsArr = data.optionals;
    },
    async createBurger() {
      const data = {
        name: this.name,
        beef: this.beef,
        bread: this.bread,
        optional: Array.from(this.optionals),
        status: this.status,
      }
      const dataJson = JSON.stringify(data);

      const req = await fetch('http://localhost:3000/burgers', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: dataJson
      })

      const response = await req.json();

      this.msg = `Obrigado ${response.name}, seu pedido Nº ${response.id} foi realizado com sucesso!`;

      setTimeout(() => this.msg = '', 5000)
      this.name = '';
      this.bread = '';
      this.beef = '';
      this.optional = '';
    },
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