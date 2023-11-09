<script lang="ts">
    
    let dados: string = "";
    let registroSelecionado: any = null;
    let resultado: any;

    function pegaCep() {
        fetch(`http://viacep.com.br/ws/${dados}/json/`).then(response => response.json())
            .then(data => {
                resultado = data;
            })
            .catch(error => {
                console.error("Erro ao buscar CEP:", error);
            });
    }
</script>

{#if resultado && resultado.cep}
    <div on:click={() => registroSelecionado = resultado}>
        <h3>{resultado.cep}</h3>
    </div>
    
    {#if registroSelecionado && registroSelecionado.cep === resultado.cep}
        <ul>
            <li>logradouro: {resultado.logradouro}</li>
            <li>complemento: {resultado.complemento}</li>
            <li>bairro: {resultado.bairro}</li>
            <li>localidade: {resultado.localidade}</li>
            <li>uf: {resultado.uf}</li>
            <li>ibge: {resultado.ibge}</li>
            <li>gia: {resultado.gia}</li>
            <li>ddd: {resultado.ddd}</li>
            <li>siafi: {resultado.siafi}</li>
        </ul>
    {/if}
{/if}

<input type="text" bind:value={dados}/>
<button type="button" on:click={pegaCep}>Buscar</button>
