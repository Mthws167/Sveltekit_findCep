<script lang="ts">
    import { onMount } from "svelte";

    let dados: any;
    let personagemSelecionado: any = null;

    onMount(async () => {
        const response = await fetch("http://rickandmortyapi.com/api/character");
        dados = await response.json();
    });
</script>

{#if dados}
    {#each dados.results as personagem (personagem.id)}
        <div on:click={() => personagemSelecionado = personagem}>
            <h3>{personagem.name}</h3>
        </div>
        
        {#if personagemSelecionado && personagemSelecionado.id === personagem.id}
            <ul>
                <li>Status: {personagem.status}</li>
                <li>Espécie: {personagem.species}</li>
                <li>Espécie: {personagem.origin.name}</li>
            </ul>
        {/if}
    {/each}
{/if}
