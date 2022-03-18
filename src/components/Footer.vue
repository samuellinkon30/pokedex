<template>
  <v-footer
    dark
    padless
  >
    <v-card
      class="flex"
      flat
      tile
    >
      <v-card-title class="teal">
        <strong class="subheading">Make with </></v-icon> and <v-icon small>mdi-heart</v-icon></strong> 

        <v-spacer></v-spacer>

        <a href="https://github.com/samuellinkon30/pokedex"
          
          v-for="icon in icons"
          :key="icon"
          class="mx-4"
          dark
          icon
          
        >
          <v-icon size="24px">
            {{ icon }}
          </v-icon>
        </a>
      </v-card-title>

      <v-card-text class="py-2 white--text text-center">
        {{ new Date().getFullYear() }} — <strong>Samuel Linkon</strong>
      </v-card-text>
    </v-card>
  </v-footer>
</template>

<script>
export default {
  name: 'Footer',
  data() {
      return{
        icons: [
        'mdi-github',
      ],
      }
  },
}
</script>
<style scoped>
footer.v-footer.v-sheet.theme--dark.v-footer--padless {
    /* position: absolute; */
    bottom: 0;
    display: block;
    width: 100%;
    /* position: fixed; */
}
</style>
