<script>
export default {
  props: {
    character: {
      type: Object,
      required: true
    },
    showButtons: {
      type: Object,
      required: false
    }
  },
  emits: ['add', 'remove'],
  methods: {
    add() {
      this.$emit('add', this.character)
    },
    remove() {
      this.$emit('remove', this.character)
    }
  }
}
</script>

<template>
  {{ character.name }} {{ character.elements.join(', ') }}
  <div>
    <button v-if="showButtons?.add" @click="add">Add</button>
    <button v-if="showButtons?.remove" @click="remove">Delete</button>
  </div>
</template>
