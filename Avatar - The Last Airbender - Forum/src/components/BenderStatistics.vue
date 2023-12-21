<script>
export default {
  props: {
    characters: {
      type: Array,
      required: true
    }
  },
  computed: {
    benderStatistics() {
      const elements = ['Water', 'Earth', 'Fire', 'Air']
      const statistics = {
        Water: 0,
        Earth: 0,
        Fire: 0,
        Air: 0
      }
      this.characters.forEach((character) => {
        elements.forEach((element) => {
          if (character.elements.indexOf(element) > -1) statistics[element] += 1
        })
      })
      return statistics
    }
  }
}
</script>

<template>
  <h3>Statistics</h3>
  <ul>
    <li v-for="(stat, type) in benderStatistics" :key="`statistics: ${type}`">
      {{ type }}: {{ stat }}
    </li>
  </ul>
</template>
