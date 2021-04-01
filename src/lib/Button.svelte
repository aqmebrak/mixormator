<script>
    import "../global.css";

    export let label = "";
    export let onClick = () => {};
</script>

<button on:click={onClick} class="border-1 bg-blue-50 rounded p-1 border-purple-100">{label}</button>

<style lang="scss">

</style>
