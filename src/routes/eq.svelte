<!-- client side only-->
<script>
  import "../global.css";
  import Button from "../lib/Button.svelte";
  import Separator from "../lib/eq/Separator.svelte";
  import VerticalCursor from "../lib/eq/VerticalCursor.svelte";
  import VerticalCursorAnswer from "../lib/eq/VerticalCursorAnswer.svelte";
  import * as Tone from "tone";

  //create a synth and connect it to the main output (your speakers)
  const player = new Tone.Player("./drums.mp3");

  // EQ
  let roundFreq = 2000;
  const bellEq = new Tone.BiquadFilter(roundFreq, "peaking").toDestination();
  bellEq.Q.value = 4;
  bellEq.gain.value = 12;
  player.connect(bellEq);

  const playSound = () => {
    Tone.loaded().then(() => {
      player.start();
    });
  };

  const stopSound = () => {
    player.stop();
  };

  const separators = [75, 100, 150, 200, 300, 400, 600, 800, 1200, 1600, 2400, 3200, 4800, 6400, 9600, 12800, 19200];

  let mouseX = null;
  let selectedFreq = null;
  let answered = false;
  const trackMouse = (event) => {
    if (!answered) {
      mouseX = event.clientX - ((window.innerWidth - 800) / 2);
    }
  };

  const answerRound = () => {
    console.log('answer');
    answered = true;
  };

</script>


<Button onClick={playSound} label="Start" />
<Button onClick={stopSound} label="Reset" />

<div class="container">
  <div class="ruler" on:mousemove={trackMouse}>
    <VerticalCursor posX={mouseX} bind:value={selectedFreq} answer={answerRound} freeze={answered} />
    {#if answered}
      <VerticalCursorAnswer value={roundFreq} />
    {/if}
    {#each separators as name, i}
      <Separator name={name} sep={i%2} />
    {/each}
  </div>
  {#if answered}
    <div class="answerContainer">{selectedFreq}</div>
  {/if}
</div>

<style lang="scss">
  .container {
    margin-left: calc((100% - 800px) / 2);
  }

  .ruler {
    position: relative;
    align-self: center;
    background-color: rgba(127, 126, 133, 0.38);
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
