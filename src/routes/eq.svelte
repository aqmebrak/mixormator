<!-- client side only-->
<script>
    import "../global.css";
    import Button from '../lib/Button.svelte';
    import * as Pizzicato from 'pizzicato';

    // vars
    let sawtoothWave =  new Pizzicato.Sound({
      source: 'wave',
      options: {
        type: 'sine'
      }
    });
    let playSound = () => sawtoothWave.play();
    let stopSound = () => sawtoothWave.stop();

</script>


  <Button onClick={playSound} label="Play"/>
  <Button onClick={stopSound} label="Stop"/>

<style lang="scss">

</style>
