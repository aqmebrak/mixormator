<script>
  import { goto } from "$app/navigation";


</script>

<div class="wrapper">
  <button
    class="cell"
    on:click={
      () => goto('eq')
    }>
    EQ Bell
  </button>
  <button
    class="cell disabled"
    on:click={
      () => goto('comp')
    }
    disabled>
    Compressor
  </button>
  <button
    class="cell disabled"
    on:click={
      () => goto('db')
    }
    disabled>
    Decibels
  </button>
</div>

<style lang="scss">
  .wrapper {
    display: flex;
    justify-content: space-around;
  }

  .cell {
    border-width: 3px;
    border-radius: 6px;
    border-color: #ab2805;
    min-height: 150px;
    width: 150px;

    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;

    font-size: 16px;
    font-weight: 700;
    color: #ab2805;
  }

  .disabled {
    border-color: rgba(44, 45, 48, 0.8);
    color: rgba(44, 45, 48, 0.8);
    cursor: unset;
  }
</style>