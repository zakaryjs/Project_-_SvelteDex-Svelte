<!-- JavaScript -->
<script>
    import { onMount } from "svelte";

    const baseUrl = "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/"

    let pokemonObj = []
    let number = '1'
    let newNumber = ''
    let pokemonName = ''
    let stats = ''
    

    async function fetchPokemonData() {
        newNumber = number
        let response = await fetch(`https://pokeapi.co/api/v2/pokemon/${newNumber}`).catch(error => error)
        let data = await response.json().catch(error => error)
        pokemonObj = data
        number = data.id
        pokemonName = data.name
        stats = data.stats
        console.log(data)
    }

    onMount(fetchPokemonData)

</script>

<!-- Markup -->
    <h1>SvelteDex</h1>
    <form on:submit={fetchPokemonData}>
        <input required type="number" min="1" max="1010" bind:value={number}>
    </form>

    <h2>{pokemonObj.name}</h2>
    <div id="img">
        <img src={`${baseUrl}${newNumber}.png`} alt="pokemon">
    </div>

    {#each stats as { base_stat, stat }, i}
    <key id={i}>
        <h3>{stat.name.toUpperCase()}: {base_stat}</h3>
    </key>
    {/each}


<!-- Styling -->
<style>
    h1 {
        text-align: center;
    }

    h3 {
        text-align: center;
    }

    form {
        text-align: center;
        scale: 1.5;
    }

    h2 {
        text-align: center;
    }

    #img {
        display: flex;
        justify-content: center;
    }

</style>