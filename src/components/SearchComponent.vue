<template>
    <div>
        <input v-model="pokemonName" placeholder="Inserisci il nome del pokemon" @keyup.enter="fetchPokemon">
        <button @click="fetchPokemon">Cerca</button>
    </div>

    <div v-if="pokemon">
        <h2>{{ pokemon.name}}</h2>
        <img :src="pokemon.sprites.front_default" alt="Pokémon Image" />
        <p><strong>Height:</strong> {{ pokemon.height }}</p>
        <p><strong>Weight:</strong> {{ pokemon.weight }}</p>
        <p><strong>Base Experience:</strong> {{ pokemon.base_experience }}</p>
    </div>

    <div v-if="error" class="error">{{ error }}</div>
</template>

<script>
import axios from 'axios';
import { capitalize } from 'vue';
    export default {
        name: 'SearchComponent',
        data() {
            return {
                pokemonName: '',
                pokemon: null,
                error: null
            }
        },
        methods: {
            async fetchPokemon(){
                const name = this.pokemonName.trim().toLowerCase();

                console.log(name);

                try{
                    this.error = null;
                    const response = await axios.get(`https://pokeapi.co/api/v2/pokemon/${name}`);
                    console.log(response.data);
                    this.pokemon = response.data;
                } catch(err){
                    this.error = 'Pokemon non trovato. Prova con un altro nome!';
                }
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>