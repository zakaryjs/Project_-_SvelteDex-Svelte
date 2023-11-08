<!-- JavaScript -->
<script>
    import { onMount } from "svelte";

    const baseUrl = "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/"

    let pokemonObj = []
    let number = '1'
    let newNumber = ''

    async function fetchPokemonData() {
        newNumber = number
        let response = await fetch(`https://pokeapi.co/api/v2/pokemon/${newNumber}`).catch(error => error)
        let data = await response.json()
        pokemonObj = data
        number = data.id
        name = data.name
    }

    onMount(fetchPokemonData)

</script>

<!-- Markup -->
<h1>Change the pokemon that is displayed! (Enter the dex number in the text box below.)</h1>
<form on:submit={fetchPokemonData}>
    <input required type="number" bind:value={number}>
</form>

<h2>{pokemonObj.name}</h2>
<img src={`${baseUrl}${newNumber}.png`} alt="pokemon">


<!-- Styling -->
<style>


</style>