<template>
  <h1>Página Sobre</h1>
</template>

<script>
export default {
  name: "About-Page",
  mounted: function(){
    let jwt = localStorage.getItem('jwt');
    if(jwt == '' || typeof jwt == 'undefined') {
      window.location.href = '#/login';
    }
  }
}
</script>

<style scoped>

</style>