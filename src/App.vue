<template>
  <Header v-bind:logo="logoSrc" v-bind:alt="appNome" />
  <router-view />
  <Footer />
</template>

<script>
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";

export default {
  name: "App",
  components: {
    Header,
    Footer,
  },
  data() {
    return {
      logoSrc: "/img/logo.png",
      appNome: "Suburguer",
    };
  },
};
</script>

<style global>
* {
  font-family: Arial, Helvetica, sans-serif;
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

.main-container {
  margin: 50px;
  min-height: 400px;
}

h1 {
  text-align: center;
  font-size: 42px;
  margin-bottom: 30px;
  color: #222;
}

/*Estilos dos botões*/

input[type="submit"],
button {
  background-color: #222;
  color: #fcba03;
  font-weight: bold;
  border: 2px solid #222;
  padding: 10px;
  font-size: 16px;
  margin: 0 auto;
  cursor: pointer;
  transition: 0.5s;
}

input[type="submit"]:hover,
button:hover {
  background-color: transparent;
  color: #222;
}
</style>
