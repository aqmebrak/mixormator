<script lang="ts">
	import "../global.css";
</script>

<nav class="flex space-x-4">
    <a class="inline-block" href=".">Home</a>
    <a class="inline-block" href="canvas">Canvas</a>
    <a class="inline-block" href="eq">EQ</a>
</nav>

<slot></slot>


<style lang="scss">
  a {
    font-size: 2rem;
    color: #ab2805;
    font-weight: 100;
    text-decoration-style: unset;
  }
</style>
