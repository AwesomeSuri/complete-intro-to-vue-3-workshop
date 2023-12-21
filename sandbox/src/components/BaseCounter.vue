<script>
export default {
  data: () => ({
    count: 0,
    incrementAmount: 1
  }),
  computed: {
    displayedTitle() {
      if (this.count > 20) return 'Counter - Large'
      return 'Counter'
    }
  },
  methods: {
    incrementCount() {
      this.count += this.incrementAmount
    }
  }
}
</script>

<template>
  <h1>{{ displayedTitle }}</h1>
  <p>{{ count }}</p>
  <button v-on:click="incrementCount">Increment</button>
  <div>
    <label for="incrementAmount">Increment by: </label>
    <input type="number" v-model="incrementAmount" />
  </div>
</template>
