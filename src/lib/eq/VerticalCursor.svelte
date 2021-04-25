<script>
  export let posX = null;

</script>

<div class="verticalCursor" style="left: {posX}px" ></div>

<style lang="scss">
.verticalCursor {
  position: absolute;
  content: '';
  top: 0;
  width: 1px;
  border-color: #802714;
  border-width: 1px;
  height: 100%;
}
</style>