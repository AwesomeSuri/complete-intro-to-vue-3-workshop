<script>
export default {
  data: () => ({
    message: 'Hello it works',
    listOfNumbers: [1, 2, 3, 4, 5, 6],
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
  <p v-if="message.length % 2 === 0">Even: {{ message }}</p>
  <p v-else>Odd: {{ message }}</p>
  <ul>
    <li v-for="(number, index) in listOfNumbers" :key="`number-${index}`">{{ number }}</li>
  </ul>
  <hr />
  <h1>{{ displayedTitle }}</h1>
  <p>{{ count }}</p>
  <button v-on:click="incrementCount">Increment</button>
  <div>
    <label for="incrementAmount">Increment by: </label>
    <input type="number" v-model="incrementAmount" />
  </div>
</template>
