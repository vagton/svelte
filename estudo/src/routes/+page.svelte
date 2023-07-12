<script>
    import { onMount } from "svelte";

    let countryCodes = [];

    onMount(async () => {
        try {
            const response = await fetch("https://restcountries.com/v3/all");
            if (response.ok) {
                const countries = await response.json();
                countryCodes = countries.map((country) => country.cca2).sort();
                console.log("Códigos de país:", countryCodes);
            } else {
                console.log("Erro na resposta da API:", response.status);
            }
        } catch (error) {
            console.log("Erro na solicitação:", error);
        }
    });

    let selectedCountryCode = "";
    let dados = {};

    async function fetchData(countryCode) {
        try {
            const response = await fetch(
                `https://servicodados.ibge.gov.br/api/v1/paises/${countryCode}`
            );
            if (response.ok) {
                const [pais] = await response.json();
                dados = pais;
                console.log("Dados:", dados);
            } else {
                console.log("Erro na resposta da API:", response.status);
            }
        } catch (error) {
            console.log("Erro na solicitação:", error);
        }
    }

    onMount(() => {
        // Chamada inicial para buscar dados do país selecionado inicialmente
        if (selectedCountryCode) {
            fetchData(selectedCountryCode);
        }
    });
</script>

<main>
    <select
        bind:value={selectedCountryCode}
        on:change={() => fetchData(selectedCountryCode)}
    >
        <option value="">Selecione um país</option>
        {#each countryCodes as code}
            <option value={code}>{code}</option>
        {/each}
    </select>

    {#if Object.keys(dados).length > 0}
        <h2>{dados.nome.abreviado}</h2>
        <p>Área total: {dados.area.total} {dados.area.unidade.nome}</p>
        <p>Região: {dados.localizacao.regiao.nome}</p>
        <p>Sub-região: {dados.localizacao["sub-regiao"].nome}</p>
        <p>Capital: {dados.governo.capital.nome}</p>
        <p>Língua: {dados.linguas[0].nome}</p>
        <p>Unidade monetária: {dados["unidades-monetarias"][0].nome}</p>
        <p>Histórico: {dados.historico}</p>
    {:else if selectedCountryCode}
        <p>Carregando dados...</p>
    {/if}
</main>
