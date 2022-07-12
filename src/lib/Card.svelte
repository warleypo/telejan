<script>
    import Card1 from '../assets/card01.jpg'
    import Card2 from  '../assets/card02.jpg'
    import Card3 from  '../assets/card03.jpg'
   // your script goes here
    export let empresa
    export let categorias
    export let telefone
    export let bgcolor = "#f1f1f1"
    export let color = "#00f"

    const images = [Card1, Card2, Card3]

    const getImage = () => images[Math.floor(Math.random() * 2.4)]
</script>

<style>
    .card {
        width: 90%;
        max-width: 300px;
        height: 151px;
        border-radius: 3px;
        border: 1px solid #c3c3c3;
        box-shadow: 2px 2px 5px rgba(0,0,0,.3);
        margin-right: .5em;
        margin-bottom: .5em;
        text-align: center;
    }

    :global(.card em) {
        color: gold;
    }
</style>

<div class="card" style="background-color: {bgcolor}; background-image: url({getImage()});">
    <h3 style="color: {color};">{@html empresa}</h3>
    <br>
    <p>{@html categorias}</p>
    <p style="text-align: right;"><a href="tel:+55{telefone}">{telefone}</a></p>
</div>