<script>
import CharacterItem from './CharacterItem.vue'

export default {
  components: {
    CharacterItem
  },
  props: {
    characters: {
      type: Array,
      required: false
    },
    showButtons: {
      type: Object,
      required: false
    }
  },
  emits: ['add', 'remove'],
  methods: {
    add(character) {
      this.$emit('add', character)
    },
    remove(character) {
      this.$emit('remove', character)
    }
  }
}
</script>

<template>
  <ul v-if="characters.length > 0">
    <li v-for="(character, index) in characters" :key="`characters: ${index}`">
      <CharacterItem
        :character="character"
        :showButtons="showButtons"
        @add="add"
        @remove="remove"
      />
    </li>
  </ul>
</template>
