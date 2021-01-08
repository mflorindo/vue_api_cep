<template>
  <div class="container">
    <div class="card">
      <div class="card-body">
        <div class="card-title">Consultar Endereço pelo CEP</div>
        <div>
          <input
            type="text"
            name="consulta_cep"
            maxlength="9"
            v-model="cep"
            class="form-control"
            placeholder="Digitar somente números"
          />
        </div>

        <div v-if="mostrar_erro">
            <div class="alert alert-danger mt-2" role="alert">
  CEP não localizado
</div>
        </div>

        <div v-if="possui_dados">
          <hr />
          <legend>Resultado</legend>

          <form>
            <div class="form-row">
              <div class="form-group col-md-6">
                <label>Logradouro</label>
                <input
                  type="text"
                  class="form-control"
                  v-model="logradouro"
                  disabled
                />
              </div>
              <div class="form-group col-md-6">
                <label>Complemento</label>
                <input
                  type="text"
                  class="form-control"
                  v-model="complemento"
                  disabled
                />
              </div>
              <div class="form-group col-md-6">
                <label>Bairro</label>
                <input
                  type="text"
                  class="form-control"
                  v-model="bairro"
                  disabled
                />
              </div>
              <div class="form-group col-md-6">
                <label for="inputAddress2">Cidade</label>
                <input type="text" class="form-control" v-model="localidade" disabled />
              </div>
            </div>
          </form>
        </div>
        <button @click="consultar()" class="btn btn-success mt-2">
          Consultar CEP
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      cep: null,
      logradouro: null,
      complemento: null,
      bairro: null,
      localidade: null,
      uf: null,
      possui_dados: false,
      mostrar_erro : null,
    };
  },
  methods: {
    consultar: function() {
      this.mostrar_erro = false
      this.possui_dados = false  
      this.axios.get(`https://viacep.com.br/ws/${this.cep}/json/`).then((response) => {
        
        this.logradouro = response.data.logradouro
        this.complemento = response.data.complemento
        this.bairro = response.data.bairro
        this.localidade = response.data.localidade
        this.possui_dados = true;

      }).catch(() => {
         this.mostrar_erro = true     
      });
    },
  },
};
</script>
