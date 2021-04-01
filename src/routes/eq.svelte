<script>
    import "../global.css";
    import { browser } from '$app/env';
    import * as Pizzicato from "pizzicato/distr/Pizzicato.js";

    if(browser){
      var sawtoothWave = new Pizzicato.Sound({
        source: 'wave',
        options: {
          type: 'sine'
        }
      });

      sawtoothWave.play();
    }

</script>

<style lang="scss">

</style>
