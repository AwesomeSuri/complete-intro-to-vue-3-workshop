<script>
import BaseCounter from './components/BaseCounter.vue'

export default {
  components: {
    BaseCounter
  },
  data: () => ({
    message: 'Hello it works',
    listOfNumbers: [1, 2, 3, 4, 5, 6]
  })
}
</script>

<template>
  <p v-if="message.length % 2 === 0">Even: {{ message }}</p>
  <p v-else>Odd: {{ message }}</p>
  <ul>
    <li v-for="(number, index) in listOfNumbers" :key="`number-${index}`">{{ number }}</li>
  </ul>
  <hr />
  <BaseCounter />
</template>
