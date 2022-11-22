<template>
  <div></div>
</template>

<script>
export default {
  name: "Sair-Page",
  mounted:function(){
    localStorage.setItem('jwt','');
    window.location.href = '#/login';
  }
}
</script>

<style scoped>

</style>