<template>
  <div id="burger-table">
    <Message :msg="msg" v-show="msg" />
    <div>
      <div id="burger-table-head">
        <div class="order-id">#</div>
        <div>Cliente</div>
        <div>Pão</div>
        <div>Carne</div>
        <div>Opcionais</div>
        <div>Ações</div>
      </div>
    </div>

    <div id="burger-table-rows">
      <div class="burger-table-row" v-for="burger in burgers" :key="burger.id">
        <div class="order-number">{{ burger.id }}</div>
        <div>{{ burger.nome }}</div>
        <div>{{ burger.pao }}</div>
        <div>{{ burger.carne }}</div>
        <div>
          <ul>
            <li v-for="(opcional, index) in burger.opcionais" :key="index">
              {{ opcional }}
            </li>
          </ul>
        </div>
        <div>
          <select
            name="status"
            class="status"
            @change="updateBurger($event, burger.id)"
          >
            <option
              v-for="s in status"
              :key="s.id"
              :value="s.tipo"
              :selected="burger.status == s.tipo"
            >
              {{ s.tipo }}
            </option>
          </select>
          <button class="delete-btn" @click="deleteBurger(burger.id)">
            Cancelar
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Message from "@/components/Message.vue";
export default {
  name: "Dashboard",
  data() {
    return {
      burgers: null,
      burger_id: null,
      status: [],
      msg: null,
    };
  },

  components: { Message },

  methods: {
    //query de select - trazer pedidos para a tabela
    async getPedidos() {
      const req = await fetch("http://localhost:3000/burgers");

      const data = await req.json();

      this.burgers = data;

      //resgatar status
      this.getStatus();
    },

    async getStatus() {
      const req = await fetch("http://localhost:3000/status");

      const data = await req.json();

      this.status = data;

      console.log(data);
    },

    //query de drop - excluir dado
    async deleteBurger(id) {
      const req = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "DELETE",
      });

      const res = await req.json();

      // colocar mensagem de sistema
      this.msg = ` Pedido removido com sucesso `;

      // limpar msg
      setTimeout(() => (this.msg = ""), 3000);

      this.getPedidos();
    },

    //query de update - mudança de status do burguer
    async updateBurger(event, id) {
      const option = event.target.value;

      const dataJson = JSON.stringify({ status: option });

      const req = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: dataJson,
      });

      const res = await req.json();

      // colocar mensagem de sistema
      this.msg = `Pedido N° ${res.id} foi atualizado para ${res.status} `;

      // limpar msg
      setTimeout(() => (this.msg = ""), 3000);

      console.log(res);
    },
  },

  mounted() {
    this.getPedidos();
  },
};
</script>



<style scoped>
#burger-table {
  max-width: 1200px;
  margin: 0 auto;
}

#burger-table-head,
#burger-table-rows,
.burger-table-row {
  display: flex;
  flex-wrap: wrap;
}

#burger-table-head {
  font-weight: bold;
  padding: 12px;
  border-bottom: 3px solid #333;
}

#burger-table-head div,
.burger-table-row div {
  width: 18%;
}

.burger-table-row {
  width: 100%;
  padding: 12px;
  border-bottom: 1px solid #333;
}

#burger-table-head .order-id,
.burger-table-row .order-number {
  width: 5%;
}

select {
  padding: 10px 5px;
  margin-right: 12px;
  border-radius: 5px;
}

.delete-btn {
  background-color: #222;
  color: #fcba09;
  font-weight: bold;
  border: 2px solid #222;
  padding: 10px 5px;
  font-size: 16px;
  margin: 0 auto;
  cursor: pointer;
  transition: 0.5s;
  border-radius: 5px;
}

.delete-btn:hover {
  background-color: transparent;
  color: #222;
}
</style>