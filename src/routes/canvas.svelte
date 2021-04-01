<script>
    import { onMount } from 'svelte';
    import { browser } from '$app/env';

    let width = 55;
    let height = 55;

    const sketch = (p5) => {
        p5.setup = () => {
            p5.createCanvas(400, 400);
        };

        p5.draw = () => {
            p5.ellipse(p5.width / 2, p5.height / 2, width, height);
        };
    };

    let P5;

    onMount(async () => {
        P5 = (await import('p5-svelte/dist/index')).default;
    });

    console.log('p5', P5);
    console.log('bro', browser)


</script>

<label>
    Width
    <input type="range" bind:value={width} min="100" max="1000" step="0.01" />
    {width}
</label>

<label>
    Height
    <input type="range" bind:value={height} min="100" max="1000" step="0.01" />
    {height}
</label>

{#if browser && P5}
<P5 {sketch} />
{/if}
