<script>
  import logo from './assets/svelte.png'
  import Counter from './lib/Counter.svelte'
  import Main from './lib/Main.svelte'
</script>

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/instantsearch.css@7.4.5/themes/satellite-min.css" integrity="sha256-TehzF/2QvNKhGQrrNpoOb2Ck4iGZ1J/DI4pkd2oUsBc=" crossorigin="anonymous">
<style>
  :global(body) {
    margin: 0;
    padding: 0;
    height: 100vh;
  }

  :global(#app) {
    height: 100%;
    width: 100%;
    display: flex;
    justify-content: center;
    background-color: #ddd;
  }

  :global(*) {
    box-sizing: border-box;
    font-family: sans-serif, Arial, Helvetica;
    font-size: 12pt;
  }
</style>

<Main />