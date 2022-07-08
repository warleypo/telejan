<script>
    import Search from "./Search.svelte"
</script>

<style>
    #container {
        width: 90%;
        max-width: 1000px;
        height: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
        background-color: #fff;
        padding: 0 1em 0 1em;
    }

    header, main, footer {
        width: 100%;
    }

    main {
        flex-grow: 1;
    }
</style>

<div id="container">
    <header>
        <h1>Telejan</h1>
    </header>

    
    <main>
        <Search />
    </main>

    
    <footer>
        <p>Telejan.com.br &copy; todos os direitos reservados</p>
    </footer>
</div>