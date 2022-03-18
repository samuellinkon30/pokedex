<template>
    <div class="header">
      <router-link to="/"><img class="logo" src="../assets/pokemon.png"/></router-link>
    </div>
</template>

<script>
export default {
  name: 'Header',
 
}
</script>

<style>
.logo{
  display: block;
  max-width: 200px;
}
.header {
    justify-content: center;
    display: flex;
    box-shadow: 0px 0px 10px 1px grey;
}
.v-toolbar__content{
  justify-content: center;
}
</style>