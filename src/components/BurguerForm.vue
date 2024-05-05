<template>
  <div>
    <Message v-bind:msg="msg" v-if="msg" />
    <div>
      <form id="burguer-form" v-on:submit="createPedido($event)">
        <div class="input-container">
          <label for="nome">Nome do cliente:</label>
          <input
            type="text"
            name="nome"
            v-model="nome"
            placeholder="Digite o seu nome"
          />
        </div>
        <div class="input-container">
          <label for="pao">Escolha o pão:</label>
          <select name="pao" v-model="pao">
            <option value="">Selecione um pão</option>
            <option
              v-for="pao in paes"
              v-bind:key="pao.id"
              v-bind:value="pao.tipo"
            >
              {{ pao.tipo }}
            </option>
          </select>
        </div>
        <div class="input-container">
          <label for="carne">Escolha a carne:</label>
          <select name="carne" v-model="carne">
            <option value="">Selecione uma carne</option>
            <option
              v-for="carne in carnes"
              v-bind:key="carne.id"
              v-bind:value="carne.tipo"
            >
              {{ carne.tipo }}
            </option>
          </select>
        </div>
        <div class="input-container" id="opcionais-container">
          <label id="label-opcionais" for="opcionais"
            >Selecione (ou não) os opcionais:</label
          >
          <div
            class="checkbox-container"
            v-for="opcional in opcionaisData"
            v-bind:key="opcional.id"
          >
            <input
              type="checkbox"
              name="opcionais"
              v-model="opcionais"
              v-bind:value="opcional.tipo"
            />
            <span>{{ opcional.tipo }}</span>
          </div>
        </div>
        <div class="input-container">
          <input type="submit" value="Criar meu burguer!" />
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import Message from "./Message.vue";

export default {
  name: "BurguerForm",
  components: {
    Message,
  },
  data() {
    return {
      //resgatar
      paes: null,
      carnes: null,
      opcionaisData: null,

      //inserir
      nome: null,
      pao: null,
      carne: null,
      opcionais: [],

      //sistema de mensagens
      msg: "",
    };
  },
  methods: {
    async getIngredientes() {
      const request = await fetch("http://localhost:3000/ingredientes");
      const data = await request.json();

      this.paes = data.paes;
      this.carnes = data.carnes;
      this.opcionaisData = data.opcionais;
    },

    async createPedido(e) {
      e.preventDefault();

      const data = {
        nome: this.nome,
        pao: this.pao,
        carne: this.carne,
        opcionais: Array.from(this.opcionais),
        status: "Solicitado",
      };

      const dataJsonToText = JSON.stringify(data);

      const request = await fetch("http://localhost:3000/pedidos", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: dataJsonToText,
      });

      const response = request.json();

      console.log(response);

      //Atribuindo uma mensagem de confirmação do sistema à propriedade "msg"
      this.msg = `Pedido de ${this.nome} realizado com sucesso!`;

      //Limpando a mensagem depois de um tempo
      setTimeout(() => {
        this.msg = "";
      }, 3000);

      //Limpando os campos de input
      this.nome = "";
      this.pao = "";
      this.carne = "";
      this.opcionais = "";
    },
  },
  mounted() {
    this.getIngredientes();
  },
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
  margin-bottom: 20px;
}

label {
  font-weight: bold;
  margin-bottom: 15px;
  color: #222;
  padding: 5px 10px;
  border-left: 4px solid #fcba03;
}

input,
select {
  padding: 5px 10px;
  width: 300px;
}

#label-opcionais {
  width: 100%;
}

#opcionais-container {
  flex-direction: row;
  flex-wrap: wrap;
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
}
</style>
