<template>
  <div class="list">
    <article v-for="item in pokemonFiltered" :key="item.id" @click="clickButton(item)"><img v-bind:src="urlImage+item.name+'.png'"><h3>{{ item.name }}</h3></article>
  </div>
</template>

<script>
/*<li v-for="item in Characters" :key="item"><h3>{{ item.name }}</h3><img v-bind:src=item.images.portrait><button v-on:click="add(item)">Ajouter</button></li>*/
import axios from 'axios'
import url from '../config/config.json'
import _ from 'lodash' 
export default {
  data:function(){ return { 
      pokemon:[], 
      allPokemon:[],
      urlImage:url.IMG_URL,
    }
  },
  props: ['pokeSearched'],
  created(){
    axios 
      .get(url.API_URL+'/pokemon?&limit=1026')
      .then((response) => {
        this.pokemon=response.data.results;
        this.allPokemon=response.data.results;
       // console.log(response);
      })
      .catch((error) => {
        console.log(error);
      })
  },
  methods:{
    clickButton: function(pokemon){
      this.$emit("showDetail",pokemon);
    }
  },
  computed:{
    pokemonFiltered(){
      let regexp = new RegExp(this.pokeSearched+'.*',"gi")
      if (this.pokeSearched == null){
        return this.pokemon;
      } else {
        return _.filter(this.pokemon, function(element){
          return regexp.test(element.name)
        })
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  grid-gap: 10px;
  width: 100%;
  max-width: 510px;
}
article {
  height: 150px;
  background-color: #efefef;
  text-align: center;
  text-transform: capitalize;
  border-radius: 5px;
  cursor: pointer;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}
h3 {
  margin: 0;
}
#scroll-trigger {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 150px;
  font-size: 2rem;
  color: #efefef;
}

img {
  width: 96px;
  height: 96px;
}
</style>

