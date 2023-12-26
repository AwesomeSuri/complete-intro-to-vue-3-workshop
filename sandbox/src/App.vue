<script>
// https://pokeapi.co/api/v2pokemon?limit=151

export default {
  data: () => ({
    pokedex: [1, 2, 3]
  }),
  methods: {
    async fetchPokemon() {
      this.pokedex = await fetch('https://pokeapi.co/api/v2/pokemon?limit=151').then((response) =>
        response.json()
      )
    }
  },
  created() {
    this.fetchPokemon()
  }
}
</script>

<template>
  <h1>Pokedex</h1>
  <pre>{{ pokedex }}</pre>
</template>
