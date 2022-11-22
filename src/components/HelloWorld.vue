<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h3>MEU IP</h3>
    <ul>
      <li>O endereço IPV6 é: <b>{{ ip }}</b></li>
    </ul>
    <h3>BITCOIN</h3>
    <ul>
      <li>O preço atual do Bitcoin é:
        <b v-if="error">Ocorreu um erro, tente novamente mais tarde.</b>
        <b v-else>US$ {{ bitcoin }}</b>
      </li>
    </ul>
    <h3>FILMES EM CARTAZ</h3>
    <ul>
      <li v-if="loading">Carregando...</li>
      <li v-else v-for="filme in filmes" :key="filme.id" class="filmes">
        <div class="filmes_itens">
          <img v-bind:src="filme.avatar" />
          <h5>{{ filme.titulo }}</h5>
        </div>
      </li>
    </ul>

  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      ip: '',
      bitcoin: '0',
      error: false,
      loading: true,
      filmes: []
    }
  },
  mounted() {
    axios
        .get('http://ip.jsontest.com/')
        .then( r => {
          this.ip = r.data.ip;
        });
    axios
        .get('https://api.coindesk.com/v1/bpi/currentprice.json')
        .then( r => {
          this.bitcoin = r.data.bpi.USD.rate_float.toFixed(2);
        })
        .catch( error => {
          this.error = true;
          console.log(error);
        })
        .finally( ()=>{
          this.loading = false;
        });
    axios
        .get('https://api.b7web.com.br/cinema/')
        .then( json => {
            this.filmes = json.data;
        })
        .finally( ()=>{
          this.loading = false;
        });
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

ul {
  list-style: none;
  margin-bottom: 50px;
}
.filmes {
  padding: 10px;
  margin: 10px;
  max-width: 300px;
  display: inline-block;
}
filmes_itens {
  display: flex;
  flex-wrap: nowrap;
}
img {
  width: 200px;
  height: 300px;
}
h5 {
  display: flex;
  text-align: center;
  justify-content: center;
}
</style>
