<template>
  <div class="home">
    <PokedexSearch/>
  </div>
</template>

<script>
// @ is an alias to /src
import PokedexSearch from '@/components/PokedexSearch.vue'

export default {
  name: 'Home',
  components: {
    PokedexSearch
  }
}
</script>
