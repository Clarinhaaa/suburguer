<template>
  <div id="burguer-table">
    <div id="burguer-table-heading">
      <div class="order-id">ID:</div>
      <div>Cliente:</div>
      <div>Pão:</div>
      <div>Carne:</div>
      <div>Opcionais:</div>
      <div>Ações:</div>
    </div>
    <div id="burguer-table-rows">
      <div
        class="burguer-table-row"
        v-for="pedido in pedidos"
        v-bind:key="pedido.id"
      >
        <div class="order-id">{{ pedido.id }}</div>
        <div>{{ pedido.nome }}</div>
        <div>{{ pedido.pao }}</div>
        <div>{{ pedido.carne }}</div>
        <div>
          <ul>
            <li
              v-for="(opcional, index) in pedido.opcionais"
              v-bind:key="index"
            >
              {{ opcional }}
            </li>
          </ul>
        </div>
        <div>
          <select
            name="status"
            class="status"
            v-on:change="updatePedido($event, pedido.id)"
          >
            <option value="">Status</option>
            <option
              v-for="st in status"
              v-bind:key="st.id"
              v-bind:value="st.tipo"
              v-bind:selected="pedido.status == st.tipo"
            >
              {{ st.tipo }}
            </option>
          </select>
          <button v-on:click="deletePedido(pedido.id)">Cancelar</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Dashboard",
  data() {
    return {
      pedidos: null,
      pedidoId: null,
      status: null,
    };
  },
  methods: {
    async getPedidos() {
      const request = await fetch("http://localhost:3000/pedidos");
      const data = await request.json();

      this.pedidos = data;

      this.getStatus();
    },

    async getStatus() {
      const request = await fetch("http://localhost:3000/status");
      const data = await request.json();

      this.status = data;
    },

    async deletePedido(id) {
      await fetch(`http://localhost:3000/pedidos/${id}`, {
        method: "DELETE",
      });

      this.getPedidos();
    },

    async updatePedido(event, id) {
      const option = event.target.value;
      const dataJsonToText = JSON.stringify({ status: option });

      const request = await fetch(`http://localhost:3000/pedidos/${id}`, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: dataJsonToText,
      });

      const response = await request.json();
      console.log(response);
    },
  },
  mounted() {
    this.getPedidos();
  },
};
</script>

<style scoped>
#burguer-table {
  max-width: 1200px;
  margin: 0 auto;
}

#burguer-table-heading,
#burguer-table-rows,
.burguer-table-row {
  display: flex;
  flex-wrap: wrap;
}

#burguer-table-heading {
  font-weight: bold;
  padding: 12px;
  border-bottom: 3px solid #333;
}

#burguer-table-heading div,
.burguer-table-row div {
  width: 18.6%;
}

.burguer-table-row {
  width: 100%;
  padding: 12px;
  border-bottom: 1px solid #ccc;
}

#burguer-table-heading .order-id,
.burguer-table-row .order-id {
  width: 7%;
}

select {
  padding: 12px 6px;
  margin-right: 12px;
}
</style>
