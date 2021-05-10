<script>
  import "../global.css";

  export let label = "";
  export let onClick = () => {
  };
</script>

<button on:click={onClick} class="border-1 bg-blue-50 rounded p-1 border-purple-100">{label}</button>

<style lang="scss">
  button {
    color: #1d2021;
    background-color: #9ca3af;
    min-width: 70px;
    min-height: 32px;

    &:hover {
      background-color: rgb(200, 200, 200);
    }
  }
</style>
