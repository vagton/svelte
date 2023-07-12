<script>
    import Layout from "./+layout.svelte";

    let pageTitle = "Minha Página";
</script>

<Layout title={pageTitle}>
    <section>
        <h2>Bem-vindo à minha página!</h2>
        <p>Este é o conteúdo da página.</p>
    </section>
</Layout>

<style>
    section {
        background-color: #f0f0f0;
        padding: 20px;
        border-radius: 4px;
    }

    h2 {
        color: #333;
        font-size: 20px;
        margin-bottom: 10px;
    }

    p {
        color: #666;
        font-size: 16px;
    }
</style>
