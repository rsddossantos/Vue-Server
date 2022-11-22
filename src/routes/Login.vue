<template>
  <h1>Login</h1>
    <p class="error" v-if="error != ''">{{error}}</p>
    <label>
      E-mail:
      <input type="email" v-model="email" />
    </label>
    <label>
      Senha:
      <input type="password" v-model="pass" />
    </label>
    <button @click="entrar">Entrar</button>
</template>

<script>

export default {
  name: "Login-Page",
  data() {
    return {
      email:'',
      pass:'',
      error: ''
    }
  },
  methods: {
    entrar: function() {
      fetch('http://localhost:4000/login', {
        method: 'POST',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify({email: this.email, password: this.pass})
      })
      .then(r=>r.json())
      .then(json=>{
         if (json.status) {
           localStorage.setItem('jwt', json.token);
           window.location.href = "#/";
           console.log(json);
         } else {
           this.error = 'Acesso Negado!';
         }
      })
      .catch(()=>{
        this.error = 'Erro na requisição, tente novamente!';
      })




    }
  }
}
</script>

<style scoped>
label {
  display:block;
  margin-top:10px;
  margin-bottom: 10px;
}
.error {
  color:#FF5555;
}
</style>