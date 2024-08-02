<script lang="ts">
  import TimerInput from "./lib/components/TimerInput.svelte";
  import TimersList from "./lib/components/TimersList.svelte";

  let newTimer = 0; // in seconds
  let timers: number[] = [];

  function addTimer(newTimer: number): void {
    timers = [...timers, newTimer];
  }
</script>

<main class="container">
  <TimerInput timer={newTimer} on:addTimer={(e) => addTimer(e.detail)} />
  <TimersList {timers} />
</main>

<style>
  .container {
    padding: 40px 30px;
    margin: 0 auto;
    max-width: 870px;
    display: flex;
    flex-direction: column;
    gap: 3rem;
  }
</style>
