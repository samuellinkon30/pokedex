<template>
<div>
    id: {{ param }}
    <PokemonView/>
</div>
</template>


<script>

import PokemonView from '../components/PokemonView.vue'

export default {
  name: 'Pokemon',
  data() {
      return {
          param:"",
      }
  },
  components: {
    PokemonView
  },
  methods:{
      getParam(){
           this.param=this.$route.query.id;
           if(this.param == ""){
                 alert("Pesquisa Invalida");

               this.$router.push('/');
            }
      },
  },
  created() {
    this.getParam();
  },
}
</script>
