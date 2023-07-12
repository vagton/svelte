<script>
    export let title = "Título da Página";
</script>

<main>
    <header>
        <h1>{title}</h1>
    </header>

    <slot />
</main>

<style>
    main {
        max-width: 800px;
        margin: 0 auto;
        padding: 20px;
    }

    header {
        text-align: center;
        margin-bottom: 20px;
    }

    h1 {
        font-size: 24px;
        color: #333;
    }
</style>
