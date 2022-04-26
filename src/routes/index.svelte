<script>
    import {pokemon} from "../stores/pokestore.js";
</script>

<h1>Svelte Kit PokeDex</h1>

{#each $pokemon as pokebeing}
    <p>{pokebeing.name}</p>
{/each}
<style>
</style>