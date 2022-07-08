<script>
    import algoliasearch from 'algoliasearch'
    import instantsearch from 'instantsearch.js'
    import { searchBox, hits } from 'instantsearch.js/es/widgets'
    import { onMount } from 'svelte';

    const appId = import.meta.env.VITE_APP_ID
    const apiKey = import.meta.env.VITE_API_KEY

    onMount(() => {
        const searchClient = algoliasearch(appId, apiKey)

        const search = instantsearch({
            indexName: 'telejan',
            searchClient,
        })

        search.addWidgets([
            searchBox({
                container: "#searchbox",
                autofocus: true,
                showLoadingIndicator: true,
                placeholder: "Busque serviço, produto ou empresa...",
            }),

            hits({
                container: "#hits",
                templates: {
                    item: `
                        <section style="width: 100%">
                            <img src="https://app.tjcampo.com/assets/images/campo.png" align="left" alt="logomarca" width="50px" />
                            <h2>{{#helpers.highlight}}{ "attribute": "empresa" }{{/helpers.highlight}}</h2>
                            <p>{{#helpers.highlight}}{ "attribute": "categoria" }{{/helpers.highlight}}</p>
                        </section>
                    `,
                    empty: "Desculpe, não localizamos nada. Tente ser mais especifico!",
                }
            }),

        ])

        search.start()
    })
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
</style>

<div id="box">

    <div class="left-panel">
        <div id="clear-filters"></div>

        <h2>Categorias</h2>
        <div id="category-list"></div>
    </div>

    <div class="right-panel">
        <div id="searchbox"></div>
        <div id="hits"></div>
        <div id="pagination"></div>
    </div>
</div>