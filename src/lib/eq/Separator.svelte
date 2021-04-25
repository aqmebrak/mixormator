<script>
  export let name = '';
  export let sep = false;
</script>

<div class="separator">
  {#if sep}
    <div class="sep"></div>
  {/if}
  <div class='text' class:offsetText={!sep}>{name}</div>
</div>

<style lang="scss">
  .separator {
    padding: 20px 0;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    flex: 1;
  }
  .text {
    padding-top: 30px;
    align-self: center;
    font-size: 11px;
    color: white;
  }
  .offsetText {
    padding-bottom: 20px;
  }

  .sep {
    flex: 1;
    border-width: 1px;
    width: 1px;
    align-self: center;
  }
</style>