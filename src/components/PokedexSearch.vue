<template>
  <v-container class=" lighten-5 full">
    <v-row no-gutters class="line">
    <div class="logoPokedex">
      <img class="logo" src="../assets/pokedex.png"/>
    </div>
    </v-row>
    <v-row no-gutters class="line">
    <div class="titlePokedex">
        <h1>Pesquise se Pokemon</h1>
    </div>
    </v-row>
    <v-row class="pesquisa">
    <v-form
    ref="form"
    lazy-validation
  >
    <v-text-field
      v-model="name"
      label="Nome do Pokemon"
      required
     
    ></v-text-field>
     <v-btn
    
      color="success"
      class="mr-4"
      @click.stop="goPage(name)"
    >
      Pesquisar
    </v-btn>
    </v-form>
    </v-row>
    <v-row class="title">
        <h3>Histórico</h3>
    </v-row>
    <v-row class="globalHistory hidden-sm-and-down">
        <div class="history" v-show="hasHistory">
           
        <div class="card" v-for="(pokemon,index) in info" :key="index" @click="goPage(pokemon.nome)">
            <Card :nome="pokemon.nome" :imagem="pokemon.imagem" />
        </div>
        </div>
    </v-row>
  </v-container>
 
</template>


<script>
import axios from 'axios';
import Card from './Card.vue';

export default {
  name: 'PokedexSearch',
  components: {
    Card,
  },
  data() {
      return {
          name:"",
          pesquisas:[],
          info:[],
          hasHistory:false,
      }
  },
  created(){
       this.verifySearch();
  },
  methods:{
    goPage(link){
        this.setStorageSearch()
        this.$router.push({ name: 'Pokemon', query: { id: link }});
        
    },
    verifySearch(){
        this.pesquisas = JSON.parse(localStorage.getItem("pesquias") || '[]')
        if(this.pesquisas!=null){
            this.hasHistory = true;
            console.log(this.pesquisas);
            this.showSearch(this.pesquisas);
        }
    },

    setStorageSearch(){
          let pesquisa = this.name;
          let pesquiaAaux = this.pesquisas;
          if(pesquiaAaux.length <= 10){
          if(!pesquiaAaux.includes(pesquisa)){
            this.pesquisas.push(pesquisa);
            localStorage.setItem("pesquias", JSON.stringify(this.pesquisas));
          }else{ console.log("N foi")}}
      },

   showSearch(history){
        console.log("info: "+history);
        let aux = history.reverse();
        console.log("Reverse: "+aux)
        aux.forEach((value, index) => {
        if(index <= 7){
        axios.get('https://pokeapi.co/api/v2/pokemon/'+value).then((response) =>{
      
      let pokemonAux = {
          nome: response.data.name,
          imagem: response.data.sprites.front_default
      };
      console.log(index);
      this.info.push(pokemonAux);
    }).catch((err)=>{
      console.log("Erro: " + err);
    });
    }
    else{
        return false;
    }

    });
 
  },
},
}
</script>
<style>
.row.title {
    text-align: center;
    display: block;
    margin: 20px 0;
}
.globalHistory{
    margin-top: 20px;
}
.history{
    text-align: center;
    display: flex;
}
.history .card{
    width: 30%;
    margin: 0 20px;
    cursor: pointer;
}
.line{
    justify-content: center;
}
.logo{
  display: block;
  max-width: 200px;
}
.logoPokedex {
    justify-content: center;
    display: flex;
    
    padding: 40px 0px;
}
.v-toolbar__content{
  justify-content: center;
}
.pesquisa{
    display: block;
}
</style>


