<script>
export default {
  data: () => ({
    characterList: [
      { name: 'Aang', elements: ['Water', 'Earth', 'Fire', 'Air'] },
      { name: 'Katara', elements: ['Water'] },
      { name: 'Zokka', elements: [] },
      { name: 'Toph', elements: ['Earth'] },
      { name: 'Zuko', elements: ['Fire'] }
    ],
    customCharacterList: [],
    favouriteList: [],
    newCharacter: {
      name: '',
      elements: {
        Water: false,
        Earth: false,
        Fire: false,
        Air: false
      }
    }
  }),
  computed: {
    benderStatistics() {
      const elements = ['Water', 'Earth', 'Fire', 'Air']
      const statistics = {
        Water: 0,
        Earth: 0,
        Fire: 0,
        Air: 0
      }
      this.favouriteList.forEach((character) => {
        elements.forEach((element) => {
          if (character.elements.indexOf(element) > -1) statistics[element] += 1
        })
      })
      return statistics
    }
  },
  methods: {
    addToFavourites(character) {
      if (!this.favouriteList.includes(character)) this.favouriteList.push(character)
    },
    removeFromFavourites(character) {
      const index = this.favouriteList.indexOf(character)
      if (index > -1) this.favouriteList.splice(index, 1)
    },
    addCustomCharacter() {
      if (this.newCharacter.name.length > 0) {
        const elements = ['Water', 'Earth', 'Fire', 'Air']
        const masteredElements = []
        elements.forEach((element) => {
          if (this.newCharacter.elements[element]) masteredElements.push(element)
        })
        const newChar = {
          name: this.newCharacter.name,
          elements: masteredElements
        }
        this.customCharacterList.push(newChar)
        this.newCharacter.name = ''
        this.newCharacter.elements = {
          Water: false,
          Earth: false,
          Fire: false,
          Air: false
        }
      }
    },
    removeCustomCharacter(character) {
      const index = this.customCharacterList.indexOf(character)
      if (index > -1) this.customCharacterList.splice(index, 1)
    }
  }
}
</script>

<template>
  <label for="character-name">New Character: </label>
  <input
    type="text"
    title="character-name"
    name="character-name"
    v-model="newCharacter.name"
    placeholder=""
  />
  <div
    v-for="(element, type) in { Water: 0, Earth: 0, Fire: 0, Air: 0 }"
    :key="`element-option: ${type}`"
  >
    <input
      type="checkbox"
      :id="`${type}`"
      :name="`${type}`"
      v-model="newCharacter.elements[type]"
    />
    <label :for="`${type}`">{{ type }}</label>
  </div>
  <button @click="addCustomCharacter">Add character</button>
  <h3>Character List:</h3>
  <p v-if="characterList.length === 0 && customCharacterList.length === 0">
    There are no characters
  </p>
  <div v-else>
    <ul v-if="characterList.length > 0">
      <li v-for="(character, index) in characterList" :key="`character-list: ${index}`">
        {{ character.name }} {{ character.elements.join(', ') }}
        <div>
          <button @click="addToFavourites(character)">Add to Favourites</button>
        </div>
      </li>
    </ul>
    <ul v-if="customCharacterList.length > 0">
      <li v-for="(character, index) in customCharacterList" :key="`custom-list: ${index}`">
        {{ character.name }} {{ character.elements.join(', ') }}
        <div>
          <button @click="addToFavourites(character)">Add to Favourites</button>
          <button @click="removeCustomCharacter(character)">Delete</button>
        </div>
      </li>
    </ul>
  </div>

  <h3>Favourite List:</h3>
  <p v-if="favouriteList.length === 0">You have no favourite characters</p>
  <ul v-else>
    <li v-for="(favourite, index) in favouriteList" :key="`favourite-list: ${index}`">
      {{ favourite.name }} {{ favourite.elements.join(', ') }}
      <div>
        <button @click="removeFromFavourites(favourite)">Remove from Favourites</button>
      </div>
    </li>
  </ul>
  <h3>Statistics</h3>
  <ul>
    <li v-for="(stat, type) in benderStatistics" :key="`statistics: ${type}`">
      {{ type }}: {{ stat }}
    </li>
  </ul>
</template>
