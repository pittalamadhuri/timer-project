<script>
    import { onDestroy, onMount } from 'svelte';
  
    let interval;
    let seconds = 0;
    let isRunning = false;
  
    function startTimer() {
      isRunning = true;
      interval = setInterval(() => {
        seconds++;
      }, 1000);
    }
  
    function stopTimer() {
      isRunning = false;
      clearInterval(interval);
    }
  
    function resetTimer() {
      seconds = 0;
      stopTimer();
    }
  
    // Cleanup function to clear interval when component is destroyed
    onDestroy(() => {
      clearInterval(interval);
    });
  </script>
  
  <style>
    .timer {
      font-size: 2em;
      text-align: center;
      margin: 20px;
    }
  
    .controls {
      display: flex;
      justify-content: center;
    }
  
    button {
      margin: 0 10px;
      padding: 10px 20px;
      font-size: 1em;
      cursor: pointer;
    }
  </style>
  
  <div class="timer">{seconds} seconds</div>
  <div class="controls">
    {#if !isRunning}
      <button on:click={startTimer}>Start</button>
    {:else}
      <button on:click={stopTimer}>Stop</button>
    {/if}
    <button on:click={resetTimer}>Reset</button>
  </div>
  