<template>
  <div class="container">
    <PokemonSearch />
    <PokemonDetail v-if="clickButton === true" @clickButton = "clickButton = false" :pokemonURL="pokemon.url"/>
    <PokemonList @showDetail="showWindow"/>
  </div>
</template>

<script>
import PokemonDetail from "../components/PokemonDetail.vue";
import PokemonList from "../components/PokemonList.vue";
import PokemonSearch from "../components/PokemonSearch.vue";

export default {
  data:function(){ return { 
      numero: 0,
      clickButton: false,
      pokemon: '',
    }
  },
  methods: {
    showWindow : function(pokemon){
      this.clickButton = true;
      this.pokemon = pokemon;
    }
  },
  components: {
    PokemonDetail,
    PokemonList,
    PokemonSearch,
  },
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 10px;
  width: calc(100% - 20px);
  min-height: calc(100vh - 20px);
  //background: radial-gradient(#ffbf0b, #e20000);

  font-family: "Acme", arial;
  font-size: 1rem;
  font-weight: normal;
}

h1 {
  color: #efefef;
}
</style>