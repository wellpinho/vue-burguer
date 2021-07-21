<template>
  <div class="main-container">
    <Message :msg="msg" v-show="msg" />
    <div id="burger-table">
      <div>
        <div id="burger-table-heading">
          <div id="order-id">#:</div>
          <div>Cliente:</div>
          <div>Pão</div>
          <div>Carne:</div>
          <div>Opcionais:</div>
          <div>Ações</div>
        </div>
      </div>

      <div 
        id="burger-table-rows"
        v-for="burger in burgers"
        :key="burger.id"
      >
        <div class="burger-table-row">
          <div class="order-number">{{ burger.id }}</div>
          <div>{{ burger.name }}</div>
          <div>{{ burger.bread }}</div>
          <div>{{ burger.beef}}</div>
          <div>
            <ul>
              <li 
                v-for="(optional, index) in burger.optional" 
                :key="index"
              >
                {{ optional }}
              </li>
            </ul>
          </div>

          <div>
            <select 
              name="status" 
              class="status"
              @change="update($event, burger.id)"
            >
              <option 
                :value="state.tipo"
                v-for="state in status"
                :key="state.id"
                :selected="burger.status === state.tipo"
              >
                {{ state.tipo }}
              </option>
            </select>
            <button 
              class="delete-btn"
              @click="deleteRequest(burger.id)"
            >
              Cancelar
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Message from './../components/Msg.vue'

export default ({
  name: 'Dashboard',
  components: {
    Message
  },
  data() {
    return {
      burgers: null,
      burger_id: null,
      status: '',
      msg: ''
    }
  },
  methods: {
    async getRequests() {
      const request = await fetch('http://localhost:3000/burgers');
      const data = await request.json();

      this.burgers = data;
      this.getStatus();
    },
    async getStatus() {
      const request = await fetch('http://localhost:3000/status');
      const data = await request.json();

      this.status = data;
    },
    async deleteRequest(id) {
      const request = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: 'DELETE'
      });

      const response = await request.json();

      this.msg = `Pedido removido com sucesso.`;
      setTimeout(() => this.msg = '', 5000);

      this.getRequests();
    },
    async update(event, id) {
      const option = event.target.value;
      const dataJson = JSON.stringify({ status: option })
      const request = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json'},
        body: dataJson
      });

      const response = await request.json();

      this.msg = `Pedido ${response.id} foi atualizado para ${response.status}.`;
      setTimeout(() => this.msg = '', 5000);

      console.log(response)

    }
  },
  mounted() {
    this.getRequests();
  }
})
</script>

<style scoped>
  #burger-table {
    max-width: 1200px;
    margin: 0 auto;
  }

  #burger-table-heading,
  #burger-table-rows,
  .burger-table-row {
    display: flex;
    flex-wrap: wrap;
  }

  #burger-table-heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
  }

  #burger-table-heading div,
  .burger-table-row div {
    width: 19%;
  }

  .burger-table-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #ccc;
  }

  #burger-table-heading .order-id,
  .burger-table-row .order-number {
    width: 5%;
  }

  select {
    padding: 12px 7px;
    margin-right: 12px;
  }

  .delete-btn {
    background-color: #222;
    color: #fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }

  .delete-btn:hover {
    border: 2px solid #fcba03;
    background-color: #fcba03;
    color: #FFF;
  }

  ul {
    list-style: none;
  }
</style>
