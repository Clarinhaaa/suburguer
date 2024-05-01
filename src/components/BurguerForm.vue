<template>
  <div>
    <p>[mensagem do sistema]</p>
    <div>
      <form id="burguer-form">
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
            <option value="italianoBranco">Italiano Branco</option>
            <option value="tresQueijos">3 Queijos</option>
          </select>
        </div>
        <div class="input-container">
          <label for="carne">Escolha a carne:</label>
          <select name="carne" v-model="carne">
            <option value="">Selecione uma carne</option>
            <option value="boi">Boi</option>
            <option value="picanha">Picanha</option>
          </select>
        </div>
        <div class="input-container" id="opcionais-container">
          <label id="label-opcionais" for="opcionais">Selecione (ou não) os opcionais:</label>
          <div class="checkbox-container">
            <input
              type="checkbox"
              name="opcionais"
              v-model="opcionais"
              value="calabresa"
            />
            <span>Calabresa</span>
          </div>
          <div class="checkbox-container">
            <input
              type="checkbox"
              name="opcionais"
              v-model="opcionais"
              value="bacon"
            />
            <span>Bacon</span>
          </div>
        </div>
        <div class="input-container">
            <input type="submit" value="Criar meu burguer!">
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "BurguerForm",
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

input, select {
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

input[type=submit] {
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

input[type=submit]:hover {
    background-color: transparent;
    color: #222;
}
</style>
