<script>
import axios from 'axios'
import CardPoke from '@/components/CardPoke.vue'

export default {
  name: 'ListPoke',
  components: { CardPoke },
  data() {
    return {
      listPoke: []
    }
  },
  async mounted() {
    try {
      for (let i = 1; i <= 20; i++) {
        const url = 'https://pokeapi.co/api/v2/pokemon/' + i
        const { data } = await axios.get(url)
        this.listPoke.push(data)
      }
    } catch (error) {
      console.error('No se pudo atrapar un pokemon')
    }
  },
  computed: {
    counter() {
      return this.listPoke.filter((pokemon) => pokemon.esCorrecto).length
    }
  },
  methods: {
    discovered(namePokemon) {
      const foundPokemon = this.listPoke.find(
        (pokemon) => pokemon.name.toLowerCase() == namePokemon
      )
      foundPokemon.esCorrecto = true
    }
  }
}
</script>
<template>
  <div class="container">
    <div class="row text-center">
      <div>
        <img src="../../public/pokemon.png" alt="pokemon" class="w-50" />
      </div>
      <h1>¿Quien es este pokemon?</h1>
      <p>Pokemones encontrados: {{ counter }}</p>
      <CardPoke
        v-for="(pokemon, idx) in listPoke"
        :key="idx"
        :namePokemon="pokemon.name"
        :imageUrl="pokemon.sprites.front_default"
        @send-name="discovered"
      />
    </div>
  </div>
</template>
<style scoped></style>
