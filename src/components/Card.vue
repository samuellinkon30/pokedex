<template>
  <v-card
    class="mx-auto"
    min-width="150"
    
  >
  <v-card-title>
     {{nome}}
    </v-card-title>
    
    <v-img
      :src="imagem"
    ></v-img>

    
  </v-card>
</template>

<script>

export default {
    name: "Card",
    props:['nome','imagem'],
};
</script>
