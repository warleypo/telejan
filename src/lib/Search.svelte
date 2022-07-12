<script>
    import algoliasearch from 'algoliasearch'
    import Card from './Card.svelte'

    const appId = import.meta.env.VITE_APP_ID
    const apiKey = import.meta.env.VITE_API_KEY
    const adminApiKey = import.meta.env.VITE_API_ADMIN_KEY

    let strSearch = ''

    const client = algoliasearch(appId, apiKey)
    const index = client.initIndex("telejan")

    let results = []

    $: if (strSearch) {
        index.search(strSearch)
            .then(({ hits }) => {
                console.log(hits)
                results = hits
            })
            .catch(err => {
                console.log(err)
            })
    }

    const objects = [
        {
            empresa: "Seu Lucca Barbearia",
            categorias: "Barbearia, Serviço",
            palavras_chave: "barbearia, corte, cabeleireiro, cabelo, barba, bigode, tingir",
        },
        {
            empresa: "Elder Ar Condicionado",
            categorias: "Refrigeração, Serviço",
            palavras_chave: "refrigerar, ar, frio, condiciondor, veiculo",
        },
    ]

    const el = (q) => document.querySelector(q)
    const newId = () => Date.now()

    function addEmpresa (ev) {
        const adminClient = algoliasearch(appId, adminApiKey)
        const adminIndex = adminClient.initIndex("telejan")
        const empresa = {
            objectID: newId(),
            empresa: el('#empresa').value,
            categorias: el('#categorias').value,
            palavras_chave: el('#palavras_chave').value,
            telefone: el('#telefone').value,
        }
        // console.log(empresa)
        adminIndex.saveObject(empresa)
            .then(savedObj => console.log('Empresa salva.', empresa))
            .catch(err => console.log('Erro ao salvar empresa.\n', err))
    }
</script>

<style>
    #box {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
    }

    #box .left-panel {
        width: 30%;
    }

    #box .right-panel {
        width: 60%;
    }

    :global(em) {
        color: blue;
    }

    .empresas {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
    }
</style>

<div id="box">

    <div class="left-panel">
        <div id="clear-filters"></div>

        <h2>Categorias</h2>
        <div id="category-list"></div>
    </div>

    <div class="right-panel">
        <div id="searchbox">
            <input type="text" bind:value={strSearch} id="search">
        </div>
        <div id="hits">
            <!-- {#each results as item}
                <p on:click={() => strSearch = item.empresa}>{@html item._highlightResult.empresa.value}</p>
            {/each} -->
        </div>
        <div id="pagination"></div>
    </div>

</div>
<div class="empresas">
    {#each results as item}
        <Card empresa={item._highlightResult.empresa.value} categorias={item._highlightResult.categorias.value} telefone={item.telefone} />
        <!-- <p>{item.empresa}<br /><small>{item.categorias}</small></p> -->
    {/each}
</div>
<hr />

<label for="empresa">Empresa</label>
<input type="text" id="empresa" value="" placeholder="Nome da empresa">
<br />
<label for="categorias">Categorias</label>
<input type="text" id="categorias" value="" placeholder="Categorias1, categoria2, ...">
<br />
<label for="palavras_chave">palavras_chave</label>
<input type="text" id="palavras_chave" value="" placeholder="p_chave1, p_chave2, ...">
<br />
<label for="telefone">telefone</label>
<input type="text" id="telefone" value="" placeholder="DDD 00000-0000">
<br />
<button on:click={addEmpresa}>Salvar</button>