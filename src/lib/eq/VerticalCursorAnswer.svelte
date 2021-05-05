<script>
  let posX = null;
  export let value = null;

  // 0 - 100Hz
  $: if (value < 100) {
    posX = value / 100 * 67.5;
  }
  // 100 - 200Hz
  $: if (value > 100 && value < 200) {
    posX = (value - 100) / (200-100) * (162.5 - 67.5) + 67.5;
  }
  // 200 - 400Hz
  $: if (value > 200 && value < 400) {
    posX = (value - 200) / (400-200) * (256.5 - 162.5) + 162.5;
  }
  // 400 - 800Hz
  $: if (value > 400 && value < 800) {
    posX = (value - 400) / (800-400) * (351.5 - 256.5) + 256.5;
  }
  // 800 - 1600Hz
  $: if (value > 800 && value < 1600) {
    posX = (value - 800) / (1600-800) * (442.5 - 351.5) + 351.5;
  }
  // 1600 - 3200Hz
  $: if (value > 1600 && value < 3200) {
    posX = (value - 1600) / (3200-1600) * (537.5 - 442.5) + 442.5;
  }
  // 3200 - 6400Hz
  $: if (value > 3200 && value < 6400) {
    posX = (value - 3200) / (6400-3200) * (630.5 - 537.5) + 537.5;
  }
  // 6400 - 12800Hz
  $: if (value > 6400 && value < 12800) {
    posX = (value - 6400) / (12800-6400) * (736.5 - 630.5) + 630.5;

  }
  // 12800 - 20000Hz
  $: if (value > 12800 && value < 20000) {
    posX = (value - 12800) / (20000-12800) * (800 - 726.5) + 726.5;
  }

</script>

<div class="verticalCursor"
     style="left: {posX}px; border-color: green;">
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