<template>
    <div class="infoPokemon">
    <router-link class="back" to="/"><p>Pesquisar outro Pokémon</p></router-link>
    <v-container class="grey lighten-5">
    <v-row no-gutters>
      <v-col
        cols="12">
        <div class="imagem">
            <img :src="imagem" />
             <img :src="imagem2" />
        </div>
    </v-col>
    <v-col
    cols="6"
    >   
        <v-card-title>Informações</v-card-title>
        <v-card
          class="pa-2"
          outlined
          tile
        >
         <span class="nameAbility"># {{pokemon.id}}</span>
        </v-card>
        <v-card
          class="pa-2"
          outlined
          tile
        >
         <span class="nameAbility">Nome: {{pokemon.name}}</span>
        </v-card>
          <v-card
          class="pa-2"
          outlined
          tile
        >
          <span class="nameAbility">Alt: {{pokemon.height}} / Peso: {{pokemon.weight}}</span>
        </v-card>

         <v-card-title>Tipo(s)</v-card-title>
        <v-card
          class="pa-2"
          outlined
          tile
          v-for="(tipo, index) in types" :key="index"
        >
         <span class="nameAbility">{{tipo.type.name}}</span>
        </v-card>

        
        <v-card-title>Habilidades</v-card-title>
        <v-card
          class="pa-2"
          outlined
          tile
          v-for="(ability, index) in abilities" :key="index"
        >
         <span class="nameAbility">{{ability.ability.name}}</span>
        </v-card>

        
    </v-col>
         <v-col
    cols="6"
    >
        <v-card-title>Movimentos</v-card-title>
        <v-card
          class="pa-2"
          outlined
          tile
          v-for="(move, index) in moves.slice(0,9)" :key="index"
        >
         <span class="nameAbility">#{{index}} {{move.move.name}}</span>
        </v-card>

        
    </v-col>

    
  
    </v-row>
  </v-container>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: "PokemonView",
    props:['nome'],
    data() {
        return {
            pokemon:null,
            nomeP:null,
            imagem:null,
            abilities:[],
            types:[],
            infos:[],
            moves:[],
        }
    },
    created(){
       this.loadPodekon(this.nome);
    },
    methods:{
        loadPodekon(pokemon){
             axios.get('https://pokeapi.co/api/v2/pokemon/'+pokemon).then((response) =>{
                    console.log(response.data)
                    this.pokemon = response.data;
                    this.nomeP =  response.data.name;
                    this.imagem = response.data.sprites.other.home.front_default;
                    this.abilities = response.data.abilities;
                    this.infos = response.data.abilities;
                    this.types = response.data.types;
                    this.moves = response.data.moves;
            }).catch((err)=>{
                
            });
        },
        hasMoves(array){
            let size = array.lenght;
        },
    }
};
</script>

<style scoped>
.imagem {
    display: block;
    text-align: center;
}
.infoPokemon span{
    text-transform: capitalize; 
}
.infoPokemon{
    margin: 20px 0px;
}
a.back {
    text-decoration: none;
    padding: 10px;
    background-color: #1e73bb;
    display: inline-block;
    line-height: 15px;
    color: #fbcc03;
    font-weight: 700;
    font-size: 20px;
    border-radius: 5px;
    margin: 0 10px;
}
a.back p{
    margin: 0;
    padding: 0;
}
</style>