<script lang="ts">
  import TimerInput from "./TimerInput.svelte";
</script>

<div class="timer">
  <div class="timer__inputsWrapper">
    <TimerInput />
    <TimerInput />
  </div>

  <button class="timer__start">Start</button>
</div>

<style>
  .timer {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2rem;
  }

  .timer__inputsWrapper {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 3rem;
  }

  .timer__start {
    font-size: 1rem;
    font-weight: 500;
    background-color: transparent;
    color: var(--color-highlight-secondary);
    border: 1px solid var(--color-border);
    border-radius: 4px;
    padding: 0.5rem 2rem;
    box-shadow: var(--box-shadow);
    cursor: pointer;
    transition: all ease-in-out 200ms;
  }

  .timer__start:hover {
    border-color: var(--color-highlight-primary);
  }
</style>
