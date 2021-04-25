<!-- client side only-->
<script>
  import "../global.css";
  import Button from "../lib/Button.svelte";
  import * as Pizzicato from "pizzicato";
  import Separator from "../lib/eq/Separator.svelte";
  import VerticalCursor from "../lib/eq/VerticalCursor.svelte";


  // vars
  let sawtoothWave = new Pizzicato.Sound({
    source: "wave",
    options: {
      type: "sine"
    }
  });
  let playSound = () => sawtoothWave.play();
  let stopSound = () => sawtoothWave.stop();

  const separators = [75,100, 150, 200, 300, 400, 600, 800, 1200, 1600,2400, 3200,4800, 6400, 9600, 12800, 19200]

  console.log(document.getElementById("ruler"));
  const trackMouse = (event) => {
    mouseX = event.clientX - ((window.innerWidth - 800) /2);
  };

  let mouseX = null;

</script>


  <Button onClick={playSound} label="Play"/>
  <Button onClick={stopSound} label="Stop"/>

  <div class="container">
    <div id="ruler" on:mousemove={trackMouse}>
      <VerticalCursor posX={mouseX}/>
      {#each separators as name, i}
        <Separator name={name} sep={i%2}/>
      {/each}
    </div>
  </div>

<style lang="scss">
  .container {
    display: flex;
    margin-left: calc((100% - 800px) /2);
  }

  #ruler {
    position: relative;
    align-self: center;
    background-color: #4b2db9;
    width: 800px;
    height: 400px;
    display: flex;
    flex-direction: row;
    border-radius: 5px;
    cursor: none;
    border-width: 1px;
    border-color: white;
  }
</style>
