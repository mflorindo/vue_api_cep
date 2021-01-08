<template>
  <div id="app">
    
    <consulta-cep/>

    <consulta-enderecos/>
    
  </div>
</template>

<script>
import ConsultaCep from './components/ConsultaCep.vue'
import ConsultaEnderecos from './components/ConsultaEnderecos.vue'

export default {
  name: 'App',
  components: {
    ConsultaCep,
    
    ConsultaEnderecos
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
