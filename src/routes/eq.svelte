<!-- client side only-->
<script>
  import "../global.css";
  import * as Tone from "tone";
  import Chance from "chance";

  import Button from "$lib/Button.svelte";
  import Separator from "$lib/eq/Separator.svelte";
  import VerticalCursor from "$lib/eq/VerticalCursor.svelte";
  import VerticalCursorAnswer from "$lib/eq/VerticalCursorAnswer.svelte";

  //create a synth and connect it to the main output (your speakers)
  const player = new Tone.Player("./drums.mp3");

  // EQ setyp
  let roundFreq = null;
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

  // EQ SLIDER setup
  const separators = [75, 100, 150, 200, 300, 400, 600, 800, 1200, 1600, 2400, 3200, 4800, 6400, 9600, 12800, 19200];
  // array of possible freqs to be chosen as the answer
  const chance = new Chance();
  const freqs = Array.from({ length: 400 }, (_, i) => i + 50);
  const weights = [
    ...Array.from({ length: 100 }, () => 1),
    ...Array.from({ length: 100 }, () => 2),
    ...Array.from({ length: 100 }, () => 2),
    ...Array.from({ length: 100 }, () => 1)
  ];

  let round = 0;
  let mouseX = null;
  let selectedFreq = null;
  let answered = false;

  // events
  const trackMouse = (event) => {
    if (!answered) {
      mouseX = event.clientX - ((window.innerWidth - 800) / 2);
    }
  };
  const initGame = () => {
    round = 1;
    roundFreq = chance.weighted(freqs, weights);
  };

  const resetGame = () => {
    round = 0;
    answered = false;
  };

  const nextRound = () => {
    answered = false;
    roundFreq = chance.weighted(freqs, weights);
    round = round + 1;
  };

  const answerRound = () => {
    answered = true;
  };

</script>

<!--TODO export component-->
<div class="scoreboard">
  Round {round}
  {#if round === 0 && !answered}
    <Button onClick={initGame} label="Play" />
  {/if}
  {#if round !== 0 && round !== 5 && answered}
    <Button onClick={nextRound} label="Next" />
  {/if}
  {#if round === 5 && answered}
    <Button onClick={resetGame} label="Reset" />
  {/if}
</div>


<div class={`container ${round === 0 ? 'disabled' : ''}`}>
  <div class="ruler" style="cursor: {answered ? 'initial': 'none'}" on:mousemove={trackMouse}>
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
  <div class="answerContainer">{roundFreq}</div>
  <div class="answerContainer">{round}</div>
</div>

<style lang="scss">
  .container {
    margin-left: calc((100% - 800px) / 2);
  }

  .container.disabled {
    display: none;
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
    border-width: 1px;
    border-color: white;
  }

  .scoreboard {
    display: flex;
    justify-content: center;
    margin: 20px 0;
  }
</style>
