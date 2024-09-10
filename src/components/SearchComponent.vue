<template>
    <div>
        <input v-model="pokemonName" placeholder="Inserisci il nome del pokemon" @keyup.enter="fetchPokemon">
        <button @click="fetchPokemon">Cerca</button>
    </div>
</template>

<script>
    export default {
        name: 'SearchComponent',
        data() {
            return {
                pokemonName: ''
            }
        },
        methods: {
            fetchPokemon(){
                const name = this.pokemonName.trim().toLowerCase();

                try{
                    const response = axios.get(`https://pokeapi.co/api/v2/pokemon/${name}`);
                    console.log(response.data);
                } catch(err){

                }
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>