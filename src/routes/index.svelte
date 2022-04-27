<script context="module">
    export async function load() {
        const url = `https://pokeapi.co/api/v2/pokemon?limit=150`;
        const res = await fetch(url);
        const data = await res.json();
        const loadPokemon = data.results.map((data, index) => {
            return {
                name: data.name,
                id: index + 1,
                image: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${
                    index + 1
                }.png`

            }
        });
        return {props: {pokemon: loadPokemon }}
    }
</script>

<script>
    // import {pokemon} from "../stores/pokestore.js";
    import PokemanCard from "../components/pokemanCard.svelte"
    export let pokemon

    let searchTerm = "";
    let filteredPokemon = [];


    $: {
        if (searchTerm) {
            filteredPokemon = pokemon.filter(pokemon => pokemon.name.toLowerCase().includes(searchTerm.toLowerCase()));
        } else {
            filteredPokemon = [...pokemon]
        }
    }
</script>

<h1 class="text-4xl text-center my-8 uppercase">Svelte Kit PokeDex</h1>
<input type="text" placeholder="Search Pokemon" class="w-full rounded-md text-lg p-4 border-2 border-gray-200"
       bind:value={searchTerm}>

<div class="grid gap-4 md:grid-cols-2 grid-cols-1 py-4">
    {#each filteredPokemon as pokeBeing}
        <PokemanCard pokeman="{pokeBeing}"/>
    {/each}
</div>
<style>
</style>