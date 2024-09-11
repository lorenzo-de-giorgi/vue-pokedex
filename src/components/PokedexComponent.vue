<template>
    <div class="pokedex-container">
      <div class="pokedex">
        <div class="left-panel">
          <div class="search-bar">
            <SearchComponent />
          </div>
          <div class="pokemon-display">
            <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/items/poke-ball.png" alt="Poké Ball" />
          </div>
          <div class="pokemon-info">
            No valid Pokémon selected!
          </div>
        </div>
        <div class="right-panel">
          <h2>My Pokémons</h2>
          <!-- Lista dei Pokémon aggiunti -->
        </div>
      </div>
    </div>
</template>
  
<script>
    import SearchComponent from './SearchComponent.vue';

    export default {
        name: 'PokedexComponent',
        components: {
            SearchComponent
        },
        data() {
            return {
                
            };
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
        height: 400px;
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
    }
}
</style>

  
  