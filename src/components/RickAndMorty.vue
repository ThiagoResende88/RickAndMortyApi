<template>
    <div>
      <h1>Personagens de Rick e Morty</h1>
      <ul>
        <li v-for="character in characters" :key="character.id" @click="selectCharacter(character)">
          <img :src="character.image" :alt="character.name" />
          <p>{{ character.name }}</p>
        </li>
      </ul>
      <CharacterModal
        v-if="selectedCharacter"
        :show="showModal"
        :character="selectedCharacter"
        @close="showModal = false"
      />
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  import CharacterModal from './CharacterModal.vue';
  
  export default {
    components: {
      CharacterModal,
    },
    data() {
      return {
        characters: [],
        selectedCharacter: null,
        showModal: false,
      };
    },
    mounted() {
      this.fetchCharacters();
    },
    methods: {
      async fetchCharacters() {
        try {
          const response = await axios.get('https://rickandmortyapi.com/api/character');
          this.characters = response.data.results;
        } catch (error) {
          console.error('Erro ao buscar personagens:', error);
        }
      },
      selectCharacter(character) {
        console.log('Character selected:', character);
        this.selectedCharacter = character;
        this.showModal = true;
      },
    },
  };
  </script>
  
  <style scoped>
  /* Adicione estilos aqui, se necessário */
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: flex;
    align-items: center;
    margin-bottom: 10px;
    cursor: pointer;
  }
  img {
    width: 50px;
    height: 50px;
    margin-right: 10px;
    border-radius: 50%;
  }
  </style>
  