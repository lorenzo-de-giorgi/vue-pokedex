<template>
    <div>
        <input v-model="pokemonName" placeholder="Inserisci il nome del pokemon" @keyup.enter="fetchPokemon">
        <button @click="fetchPokemon"><i class="fa-solid fa-magnifying-glass"></i> | Cerca</button>
    </div>
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

                    this.$emit('pokemon-selected', {
                        name: this.pokemon.name,
                        imageUrl: this.pokemon.sprites.front_default,
                        height: this.pokemon.height,
                        weight: this.pokemon.weight,
                        baseExperience: this.pokemon.base_experience
                    })
                } catch(err){
                    this.error = 'Pokemon non trovato. Prova con un altro nome!';
                }
            }
        },
    }
</script>

<style lang="scss" scoped>

    input {
        flex: 1;
        padding: 10px;
        border: 2px solid #333;
        border-radius: 5px 0 0 5px;
        font-size: 16px;
    }

    button {
        padding: 12px;
        background-color: #333;
        border: none;
        border-radius: 0 5px 5px 0;
        cursor: pointer;
    }

</style>