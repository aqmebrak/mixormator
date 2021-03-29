<script lang="ts">
	import Header from '$lib/Header.svelte';
</script>

<main>
	<Header />

</main>

<style lang="scss">
	:root {
		font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell,
			'Open Sans', 'Helvetica Neue', sans-serif;
		background-color: #1d2021;

	}

	main {
		@apply text-center;
		@apply p-4;
		@apply mx-auto;
	}

</style>
