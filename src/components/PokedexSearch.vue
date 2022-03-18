<template>
  <v-container class=" lighten-5 full">
    <v-row no-gutters class="line">
    <div class="logoPokedex">
      <img class="logo" src="../assets/pokedex.png"/>
    </div>
    </v-row>
    <v-row no-gutters class="line">
    <div class="titlePokedex">
        <h1>Pesquise seu Pokémon</h1>
    </div>
    </v-row>
    <v-row align:center class="pesquisa">
    <v-form
    ref="form"
    lazy-validation
  >
    <v-text-field
      v-model="name"
      label="Nome do Pokémon"
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
    <v-row class="title" v-show="hasHistory">
        <h3>Histórico{{hasHistory}}</h3>
    </v-row>
    <v-row class="globalHistory hidden-sm-and-down">
        <div class="history" v-show="hasHistory">
           
        <div class="card" v-for="(pokemon,index) in info" :key="index" @click="goPage(pokemon.nome)">
            <Card :nome="pokemon.nome" :imagem="pokemon.imagem" />
        </div>
        </div>
    </v-row>

      <v-row class="globalHistoryMobile hidden-lg-and-up">
        <div class="history" v-show="hasHistory">
           
        <div class="card" v-for="(pokemon,index) in info" :key="index" @click="goPage(pokemon.nome)">
            <Card :nome="pokemon.nome" :imagem="pokemon.imagem" />
        </div>
        </div>
    </v-row>

    <div class="error" v-show="error">
          <v-alert
      color="red"
      dark
    >
     Pokémon "{{name}}" não encontrado
    </v-alert>
    </div> 

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
          error:false,
      }
  },
  created(){
       this.verifySearch();
  },
  methods:{
    goPage(link){
        
    axios.get('https://pokeapi.co/api/v2/pokemon/'+link).then((response) =>{
        this.setStorageSearch()
        this.$router.push({ name: 'Pokemon', query: { id: link }});
    }).catch((err)=>{
        this.error = true;
        setInterval(this.ocultar, 4000);
      console.log("Erro: " + err);
    });
    },
    ocultar(){
        this.error = false;
    },
    verifySearch(){
        this.pesquisas = JSON.parse(localStorage.getItem("pesquias") || '[]')
        if(this.pesquisas.length!=0){
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
        if(index <= 6){
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
    else{return false;}
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
    flex-wrap: wrap;
    width: 100%;

}
.history .card{
      width: 13%;
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
.row.globalHistory.hidden-sm-and-down {
    justify-content: center;
        margin: 33px 0px;
}
.history .v-card__title {
    justify-content: center;
    text-transform: capitalize;
}
.error {
    position: absolute;
    top: 10px;
    right: 30px;
}
@media only screen and (max-width:600px){
    .history .card {
    width: 45%;
    margin: 6px 11px;
    cursor: pointer;
}
.history {
    text-align: center;
    display: flex;
    flex-wrap: wrap;
}
.pesquisa {
    padding: 5px 20px;
}
}
</style>


