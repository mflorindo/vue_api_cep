<template>
  <div class="container">
    <div class="card">
      <div class="card-body">
        <div class="card-title">Consultar Endereço pela sigla do estado,cidade e bairro</div>
        <div>
           <form>
            <div class="form-row">
              <div class="form-group col-md-1">
                <label>Sigla</label>
                <input
                  type="text"
                  class="form-control"
                  v-model="consulta_sigla"
                  maxlength="2"
                />
              </div>
              <div class="form-group col-md-4">
                <label>Cidade</label>
                <input
                  type="text"
                  class="form-control"
                  v-model="consulta_cidade"
                  maxlength="30"                  
                />
              </div>
              <div class="form-group col-md-4">
                <label>Logradouro</label>
                <input
                  type="text"
                  class="form-control"
                  v-model="consulta_logradouro"
                  maxlength="30"
                />
              </div>
            </div>
          </form>
        </div>

        <div v-if="mostrar_erro">
            <div class="alert alert-danger mt-2" role="alert">
  Endereços não localizados
</div>
        </div>

        <div v-if="possui_dados">
          <hr />
          <legend>Resultado</legend>

          <table class="table  table-hover table-sm">
  <thead class="thead-dark">
    <tr>
      <th scope="col">CEP</th>
      <th>Estado</th>
      <th scope="col">Logradouro</th>
      <th scope="col">Complemento</th>
      <th scope="col">Bairro</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="item in resultado" :key="item.id">
        
        <td>{{ item.cep }}</td>
        <td align="left">{{item.localidade}}</td>
        <td align="left">{{ item.logradouro }}</td>
        <td align="left">{{ item.complemento }}</td>
        <td align="left">{{ item.bairro }}</td>
    </tr>
  </tbody>
</table>


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
      consulta_cidade: null,
      consulta_sigla: null,
      consulta_logradouro: null,
      logradouro: null,
      complemento: null,
      bairro: null,
      localidade: null,
      uf: null,

      possui_dados: false,
      mostrar_erro : null,
      resultado : null
    };
  },
  methods: {
    consultar: function() {
      this.mostrar_erro = false
      this.possui_dados = false  
      this.axios.get(`https://viacep.com.br/ws/${this.consulta_sigla}/${this.consulta_cidade}/${this.consulta_logradouro}/json/`).then((response) => {
      
          console.log(response.data)
        this.resultado = response.data  

        if (length(this.resultad)>0)
            this.possui_dados = true;
        else {
            this.mostrar_erro = true
            this.limpar()

        }

      }).catch(() => {
         this.mostrar_erro = true     
         this.limpar()
      });
    },
    limpar: function(){
        this.consulta_cidade = null
        this.consulta_sigla = null
        this.consulta_logradouro = null

    }
  },
};
</script>
