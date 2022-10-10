<template>
  <h1 class="fade-in">Who is that Pokemon?</h1>

  <PokemonPicture :pokemonId="6" :showPokemon="true"/>

  <PokemonOptions />
</template>

<script>
import PokemonPicture from '@/components/PokemonPicture.vue';
import PokemonOptions from '@/components/PokemonOptions.vue';
export default {
    components: { PokemonPicture, PokemonOptions }
}
</script>

<style>

</style>