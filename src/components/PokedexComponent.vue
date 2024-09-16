<template>
  <div class="pokedex-container">
    <div class="pokedex">
      <div class="left-panel">
        <div class="search-bar">
          <SearchComponent @pokemon-selected="updatePokemonDisplay" />
        </div>
        <div class="pokemon-display">
          <img :src="selectedPokemon.imageUrl" alt="Pokémon Image" v-if="selectedPokemon.imageUrl" />
          <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/items/poke-ball.png" alt="Poké Ball" v-else />
        </div>
        <div class="pokemon-info">
          <p v-if="selectedPokemon.name"><strong>Name:</strong> {{ selectedPokemon.name }}</p>
          <p v-if="selectedPokemon.height"><strong>Height:</strong> {{ selectedPokemon.height }}</p>
          <p v-if="selectedPokemon.weight"><strong>Weight:</strong> {{ selectedPokemon.weight }}</p>
          <p v-if="selectedPokemon.baseExperience"><strong>Base Experience:</strong> {{ selectedPokemon.baseExperience }}</p>
          <p v-else>No valid Pokémon selected!</p>
        </div>
        <button class="btn btn-primary mt-3" @click="addPokemon">Add to My Pokémons</button>
        <FooterComponent />
      </div>
      <div class="right-panel">
        <h2>My Pokémons</h2>
        <!-- Lista dei Pokémon aggiunti -->
        <div v-if="myPokemons.length > 0">
          <ul>
            <li v-for="(pokemon, index) in myPokemons" :key="index">
              <strong>{{ pokemon.name }}</strong> - Height: {{ pokemon.height }}, Weight: {{ pokemon.weight }} <button @click="removePokemon(index)" class="btn btn-danger ms-2"><i class="fa-solid fa-trash"></i></button>
            </li>
          </ul>
        </div>
        <p v-else>No Pokémon added yet!</p>
      </div>
    </div>
  </div>
  <footer>
    
  </footer>
</template>

<script>
import FooterComponent from './FooterComponent.vue';
import SearchComponent from './SearchComponent.vue';

export default {
  name: 'PokedexComponent',
  components: {
    SearchComponent,
    FooterComponent
  },
  data() {
    return {
      selectedPokemon: {
        name: '',
        imageUrl: '',
        height: '',
        weight: '',
        baseExperience: ''
      },
      myPokemons: []
    };
  },
  methods: {
    updatePokemonDisplay(pokemon) {
      if (pokemon) {
        this.selectedPokemon = pokemon;
      } else {
        this.selectedPokemon = {
          name: '',
          imageUrl: '',
          height: '',
          weight: '',
          baseExperience: ''
        };
      }
    },
    
    addPokemon() {
      if (this.selectedPokemon.name) {
        this.myPokemons.push({ ...this.selectedPokemon });
        localStorage.setItem('myPokemons', JSON.stringify(this.myPokemons));
        console.log('Pokémon aggiunto e salvato nel localStorage!');
      } else {
        console.log('Nessun Pokémon selezionato!');
      }
    },
    
    loadMyPokemons() {
      const savedPokemons = localStorage.getItem('myPokemons');
      if (savedPokemons) {
        this.myPokemons = JSON.parse(savedPokemons);
      } else {
        console.log('Nessun Pokémon salvato nel localStorage.');
      }
    },

    removePokemon(index){
      this.myPokemons.splice(index, 1);
      localStorage.setItem('myPokemons', JSON.stringify(this.myPokemons));
    }
  },
  // Quando il componente viene montato, carica i Pokémon dal localStorage
  mounted() {
    this.loadMyPokemons();
  }
};
</script>

<style lang="scss" scoped>

  .pokedex-container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #f0f0f0;
  }

  .pokedex {
    display: flex;
    width: 800px;
    height: 600px;
    background-color: #cc0000;
    border-radius: 15px;
    padding: 20px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);

    .left-panel, .right-panel {
      flex: 1;
      padding: 20px;
    }

    .left-panel {
      background-color: #b30000;
      border-radius: 10px;
      display: flex;
      flex-direction: column;
      align-items: center;

      .search-bar {
        display: flex;
        width: 100%;
        margin-bottom: 20px;
      }

      .pokemon-display {
        background-color: #fff;
        border-radius: 10px;
        padding: 10px;
        width: 100%;
        text-align: center;
        margin-bottom: 20px;

        img {
          width: 100px;
          height: 100px;
        }
      }

      .pokemon-info {
        background-color: #00cc00;
        border-radius: 10px;
        padding: 10px;
        width: 100%;
        text-align: center;
        color: #000;
        font-weight: bold;
      }
    }

    .right-panel {
      background-color: #ffffff;
      border-radius: 10px;
      padding: 20px;
      text-align: center;

      h2 {
        font-size: 1.5rem;
        margin-bottom: 20px;
      }

      ul {
        list-style-type: none;
        padding: 0;

        li {
          margin-bottom: 10px;
          background-color: #f0f0f0;
          padding: 10px;
          border-radius: 5px;
        }
      }
    }
  }
</style>
