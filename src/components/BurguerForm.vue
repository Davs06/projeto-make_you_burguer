<template>
  <div>
    <Message :msg="msg" v-show="msg"/>
    <form action="" id="burguer-form" @submit="createBurger">
      <div class="input-container">
        <label for="nome">Nome:</label>
        <input
          type="text"
          name="nome"
          id="nome"
          v-model="nome"
          placeholder="Digite seu Nome"
        />
      </div>

      <div class="input-container">
        <label for="pao">Escolha o pão</label>
        <select name="pao" id="pao" v-model="pao">
          <option value="" selected>Selecione seu Pão</option>
          <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">
            {{ pao.tipo }}
          </option>
        </select>
      </div>

      <div class="input-container">
        <label for="carne">Escolha a carne</label>
        <select name="carne" id="carne" v-model="carne">
          <option value="" selected>Selecione a carne</option>
          <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">
            {{ carne.tipo }}
          </option>
        </select>
      </div>

      <div class="input-container" id="opcionais-container">
        <label id="opcionais-title" for="opcionais">Escolha os opcionais</label>
        <div
          class="checkbox-container"
          v-for="opcional in opcionaisdata"
          :key="opcional.id"
        >
          <input
            type="checkbox"
            name="opciionais"
            v-model="opcionais"
            :value="opcional.tipo"
          />
          <span>{{ opcional.tipo }}</span>
        </div>
      </div>

      <div class="input-submit">
        <input type="submit" value="Criar meu Burguer" class="submit-btn" />
      </div>
    </form>
  </div>
</template>

<script>
import Message from './Message.vue';

export default {
    name: "BurguerForm",
    data() {
        return {
            paes: null,
            carnes: null,
            opcionaisdata: null,
            nome: null,
            pao: null,
            carne: null,
            opcionais: [],
            status: "Solicitado",
            msg: null,
        };
    },
    methods: {
        //query para trazer dados para o select 
        async getIngredientes() {
            const req = await fetch("http://localhost:3000/ingredientes");
            const data = await req.json();
            this.paes = data.paes;
            this.carnes = data.carnes;
            this.opcionaisdata = data.opcionais;
        },
        //query para fazer post (insert) -- pedido do burguer 
        async createBurger(e) {
            e.preventDefault();
            const data = {
                nome: this.nome,
                carne: this.carne,
                pao: this.pao,
                opcionais: Array.from(this.opcionais),
                status: "Solicitado",
            };
            const dataJson = JSON.stringify(data);
            const req = await fetch("http://localhost:3000/burgers", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            });
            const res = await req.json();
            // colocar mensagem de sistema
            this.msg = `Pedido N° ${res.id} realizado com sucesso `


            // limpar msg
            setTimeout(()=> this.msg = "", 3000)
            // limpar campos
            this.nome = "";
            this.carne = "";
            this.pao = "";
            this.opcionais = "";
        },
    },
    mounted() {
        this.getIngredientes();
    },
    components: { Message }
};
</script>

<style scoped>
#burguer-form {
  max-width: 400px;
  margin: 0 auto;
}

.input-container {
  display: flex;
  flex-direction: column;
  margin-top: 50px;
}

label {
  font-weight: bold;
  margin-bottom: 15px;
  color: #222;
  padding: 5px 10px;
  border-left: 4px solid #fcba09;
}

input,
select {
  padding: 5px 10xp;
  width: 300px;
  height: 30px;
  border-radius: 5px;
}

#opcionais-container {
  flex-direction: row;
  flex-wrap: wrap;
}

#opcionais-title {
  width: 100%;
}

.checkbox-container {
  display: flex;
  align-items: flex-start;
  width: 50%;
  margin-bottom: 20px;
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
  color: #fcba09;
  font-weight: bold;
  border: 2px solid #222;
  padding: 0 10px;
  font-size: 16px;
  margin: 0 auto;
  cursor: pointer;
  transition: 0.5s;
}

.submit-btn:hover {
  background-color: transparent;
  color: #222;
}
</style>