<script>
import CharacterList from './components/CharacterList.vue'
import BenderStatistics from './components/BenderStatistics.vue'
import BaseLayout from './components/BaseLayout.vue'

export default {
  components: {
    CharacterList,
    BenderStatistics,
    BaseLayout
  },
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

  <BaseLayout>
    <template v-slot:one>
      <h3>Character List:</h3>
      <p v-if="characterList.length === 0 && customCharacterList.length === 0">
        There are no characters
      </p>
      <div v-else>
        <CharacterList
          :characters="characterList"
          :showButtons="{ add: true }"
          @add="addToFavourites"
        />
        <CharacterList
          :characters="customCharacterList"
          :showButtons="{ add: true, removeCharacte: true }"
          @add="addToFavourites"
          @remove="removeCustomCharacter"
        />
      </div>
    </template>
    <template v-slot:two>
      <h3>Favourite List:</h3>
      <p v-if="favouriteList.length === 0">You have no favourite characters</p>
      <div v-else>
        <CharacterList
          :characters="favouriteList"
          :showButtons="{ remove: true }"
          @remove="removeFromFavourites"
        />
      </div>
    </template>
  </BaseLayout>

  <BenderStatistics :characters="favouriteList" />
</template>
