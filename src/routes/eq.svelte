<!-- client side only-->
<script>
  import { onMount } from 'svelte';
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

    let mousePos = { x: 0, y: 0 };
    var raf;
    var running = false;

    const handleMousemove = (event) => {
      const rect = document.getElementById('eq-canvas').getBoundingClientRect();
      mousePos.x = event.clientX - rect.left;
      mousePos.y = event.clientY - rect.top;
    }

    const selector = {
      x: 800/2,
      y: 400/2,
      radius: 25,
      color: 'blue',
      draw:  function(ctx) {
        ctx.beginPath();
        ctx.arc(this.x, this.y, this.radius, 0, Math.PI*2, true);
        ctx.closePath();
        ctx.fillStyle = this.color;
        ctx.fill();
      }
    }

    onMount(async () => {
      var canvas = document.getElementById('eq-canvas');
      const rect = canvas.getBoundingClientRect();

      canvas.addEventListener('mousemove', function(e){
        var ctx = canvas.getContext('2d');
        if (!running) {
          ctx.fillStyle = 'rgba(255,255,255,0.3)';
          ctx.fillRect(0,0,canvas.width,canvas.height);
          selector.x = e.clientX - rect.left;
          selector.y = e.clientY - rect.top;
          selector.draw(ctx);
        }
      });
    });



    const drawRuler = () => {
      var canvas = document.getElementById('eq-canvas');
      if (canvas.getContext) {
        var ctx = canvas.getContext('2d');
        //clear
        ctx.fillStyle = 'rgba(255,255,255,0.3)';
        ctx.fillRect(0,0,canvas.width,canvas.height);

        // tracage de 0Hz à 20kHz, palier de 500Hz
        for(let i=0; i < 20000/500; i++){
          const offsetX = i === 0 ? 0: i* 20;
          ctx.beginPath();
          ctx.moveTo(offsetX, i%2 === 0 ? 4 : 25);
          ctx.lineTo(offsetX, i%2 === 0 ? canvas.clientHeight - 4 : canvas.clientHeight - 25);
          ctx.stroke();
        }


        selector.draw(ctx);
        raf = window.requestAnimationFrame(drawRuler);
      }
    }

</script>


  <Button onClick={playSound} label="Play"/>
  <Button onClick={stopSound} label="Stop"/>

  <div class="mouse">Mouse pos: {mousePos.x} | {mousePos.y}</div>

  <canvas id="eq-canvas" width="800" height="400" on:mousemove={handleMousemove} on:load={drawRuler()}></canvas>

<style lang="scss">
  #eq-canvas {
    background-color: #9ca3af;
    margin: auto;
  }

  .mouse {
     color: white;
  }
</style>
