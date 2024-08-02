<script lang="ts">
  import { createEventDispatcher } from "svelte";
  import TimerInputItem from "./TimerInputItem.svelte";

  export let timer: number = 0;

  const dispatch = createEventDispatcher();

  let minutes: number;
  let minutesAddDisabled = false;
  let minutesSubtractDisabled = false;

  let seconds: number;
  let secondsAddDisabled = false;
  let secondsSubtractDisabled = false;

  $: {
    minutes = Math.floor(timer / 60);
    seconds = timer % 60;

    secondsSubtractDisabled = seconds === 0;
    secondsAddDisabled = minutes === 59 && seconds === 59;

    minutesSubtractDisabled = minutes === 0;
    minutesAddDisabled = minutes === 59;
  }

  function minutesChanged(e: CustomEvent): void {
    const seconds = e.detail * 60;
    timer += seconds;
  }

  function secondsChanged(e: CustomEvent): void {
    timer += e.detail;
  }

  function handleStartClick(): void {
    dispatch("addTimer", timer);
    timer = 0;
  }
</script>

<div class="timer">
  <div class="timer__inputsWrapper">
    <TimerInputItem
      value={minutes}
      valueType="M"
      addDisabled={minutesAddDisabled}
      subtractDisabled={minutesSubtractDisabled}
      on:valueChanged={minutesChanged}
    />

    <TimerInputItem
      value={seconds}
      valueType="S"
      addDisabled={secondsAddDisabled}
      subtractDisabled={secondsSubtractDisabled}
      on:valueChanged={secondsChanged}
    />
  </div>

  <button
    class="timer__start"
    on:click={handleStartClick}
    disabled={timer === 0}
  >
    Start
  </button>
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

  .timer__start:hover:not(:disabled) {
    border-color: var(--color-highlight-primary);
  }

  .timer__start:disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }
</style>
