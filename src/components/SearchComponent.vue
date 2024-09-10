<template>
    <div>
        <input v-model="pokemonName" placeholder="Inserisci il nome del pokemon" @keyup.enter="">
        <button @click="">Cerca</button>
    </div>
</template>

<script>
    export default {
        name: 'SearchComponent'
    }
</script>

<style lang="scss" scoped>

</style>