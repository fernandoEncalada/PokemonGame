<template>
  <h1 v-if="!pokemon">Wait please...</h1>

  <div v-else>
    <h1 class="fade-in">Who is that Pokemon?</h1>

    <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon"/>

    <PokemonOptions :pokemons="pokemonArr" @selection-pokemon="checkAnswer" />


    <template class="fade-in" v-if="showAnswer">
      <h2>{{ message }}</h2>
      <button @click="newGame">
        New Game
      </button>
    </template>
  </div>

</template>

<script>
import PokemonPicture from '@/components/PokemonPicture.vue'
import PokemonOptions from '@/components/PokemonOptions.vue'
import getPokemonOptions from '@/helpers/getPokemonOptions'
export default {
    components: { PokemonPicture, PokemonOptions },
    data(){
      return {
        pokemonArr: [],
        pokemon: null,
        showPokemon: false,
        showAnswer: false,
        message: ''
      }
    },
    methods: {
      async mixPokemonArray(){
        this.pokemonArr = await getPokemonOptions()

        const rndInt = Math.floor( Math.random() * 4)
        this.pokemon = this.pokemonArr[rndInt]
      },
      checkAnswer(selectedId){
        this.showPokemon = true
        this.showAnswer = true

        if(selectedId === this.pokemon.id){
          this.message = `Correct, ${this.pokemon.name}`
        }else{
          this.message = `Incorrect, was ${this.pokemon.name}`
        }
      },
      newGame(){
        this.showPokemon = false
        this.showAnswer = false
        this.pokemonArr = []
        this.pokemon = null
        this.mixPokemonArray()
      }
    },
    mounted() {
      this.mixPokemonArray()
    }
}
</script>

<style>

</style>