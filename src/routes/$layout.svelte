<script>
	import "../global.css";
</script>

<nav class="flex flex-1 justify-center space-x-4">
    <a class="inline-block special self-center" href=".">MixorMator</a>
    |
    <a class="inline-block" href="canvas">anvas</a>
    |
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

  .special {
      color: #421bcd;
      font-size: 1.9rem;
      font-weight: 100;
      //line-height: 1.1;
  }

  :root {
      font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell,
      'Open Sans', 'Helvetica Neue', sans-serif;
      background-color: #1d2021;

  }

</style>
