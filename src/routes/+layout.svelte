<script>
    import "../app.css";
</script>
  
<slot />

<style>
    :global(body) {
        padding: 2rem;
        background-color: rgb(0, 35, 48);
        font-family: Arial, Helvetica, sans-serif;
        color: aliceblue;
    }

    :global(input, button) {
        border-radius: 1rem;
    }

</style>