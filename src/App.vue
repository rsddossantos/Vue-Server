<!--<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
</template>-->

<template>
  <a href="#/login">Login</a> |
  <a href="#/">Home</a> |
  <a href="#/about">About</a> |
  <a href="#/non-existent-path">Broken Link</a> |
  <a href="#/sair">Sair</a>
  <component :is="currentView" />
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import Home from './routes/Home.vue'
import About from './routes/About.vue'
import Login from './routes/Login.vue'
import NotFound from './routes/NotFound.vue'
import Sair from './routes/Sair.vue'

const routes = {
  '/': Home,
  '/about': About,
  '/login': Login,
  '/sair': Sair
}

export default {
  name: 'App',
  data() {
    return {
      currentPath: window.location.hash
    }
  },
  computed: {
    currentView() {
      return routes[this.currentPath.slice(1) || '/'] || NotFound
    }
  },
  mounted() {
    window.addEventListener('hashchange', () => {
      this.currentPath = window.location.hash
    })
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
