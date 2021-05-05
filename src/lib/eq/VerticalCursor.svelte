<script>
  export let posX = null;
  export let value = null;
  export let freeze = false;
  export let answer = () => null;

  // 0 - 100Hz
  $: if (posX < 67.5) {
    value = posX / 67.5 * 100;
  }
  // 100 - 200Hz
  $: if (posX > 67.5 && posX < 162.5) {
    value = (posX - 67.5) / 91 * (200 - 100) + 100;
  }
  // 200 - 400Hz
  $: if (posX > 162.5 && posX < 256.5) {
    value = (posX - 162.5) / 91 * (400 - 200) + 200;
  }
  // 400 - 800Hz
  $: if (posX > 256.5 && posX < 351.5) {
    value = (posX - 256.5) / 91 * (800 - 400) + 400;
  }
  // 800 - 1600Hz
  $: if (posX > 351.5 && posX < 442.5) {
    value = (posX - 351.5) / 91 * (1600 - 800) + 800;
  }
  // 1600 - 3200Hz
  $: if (posX > 442.5 && posX < 537.5) {
    value = (posX - 442.5) / 91 * (3200 - 1600) + 1600;
  }
  // 3200 - 6400Hz
  $: if (posX > 537.5 && posX < 630.5) {
    value = (posX - 537.5) / 91 * (6400 - 3200) + 3200;
  }
  // 6400 - 12800Hz
  $: if (posX > 630.5 && posX < 726.5) {
    value = (posX - 630.5) / 91 * (12800 - 6400) + 6400;
  }
  // 12800 - 20000Hz
  $: if (posX > 726.5 && posX < 800) {
    value = (posX - 726.5) / 91 * (20000 - 12800) + 12800;
  }

</script>

<div class="verticalCursor"
     style="left: {posX}px; border-color: {freeze ? 'grey': '#802714'};"
     on:click={answer}>
</div>

<style lang="scss">
  .verticalCursor {
    position: absolute;
    content: '';
    top: 0;
    width: 1px;
    border-width: 2px;
    height: 100%;
  }
</style>