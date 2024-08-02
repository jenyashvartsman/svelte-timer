<script lang="ts">
  import { createEventDispatcher } from "svelte";

  export let timer: number;

  const dispatch = createEventDispatcher();

  let timeLeft: number = timer;
  let activeWidth: string;
  let timerInterval: number | undefined;

  let isPaused = false;

  $: {
    activeWidth = `${((timeLeft / timer) * 100).toFixed(2)}%`;
  }

  $: format = (): string => {
    const minutes = Math.floor(timeLeft / 60);
    const seconds = timeLeft % 60;
    return `${minutes > 9 ? minutes : "0" + minutes} minutes ${seconds > 9 ? seconds : "0" + seconds} seconds`;
  };

  startTimer();

  function startTimer(): void {
    timerInterval = setInterval(() => {
      timeLeft = timeLeft - 1;

      if (timeLeft <= 0) {
        stopTimer();
      }
    }, 1_000);
  }

  function stopTimer(): void {
    clearInterval(timerInterval);
  }

  function handlePauseClick(): void {
    isPaused = true;
    stopTimer();
  }

  function handlePlayClick(): void {
    isPaused = false;
    startTimer();
  }

  function handleDeleteClick(): void {
    // todo
  }
</script>

<div class="card">
  <div class="card__top">
    <h3 class="card__timeLeft">
      {#if timeLeft > 0}
        <span class="material-symbols-outlined"> notifications </span>
      {:else}
        <span class="material-symbols-outlined active">
          notifications_active
        </span>
      {/if}
      <span>{format()}</span>
    </h3>
    <div class="card_actions">
      {#if timeLeft > 0}
        {#if isPaused}
          <button class="card__btn" on:click={handlePlayClick}>
            <span class="material-symbols-outlined"> play_circle </span>
          </button>
        {:else}
          <button class="card__btn" on:click={handlePauseClick}>
            <span class="material-symbols-outlined"> pause_circle </span>
          </button>
        {/if}
      {/if}

      <button class="card__btn" on:click={handleDeleteClick}>
        <span class="material-symbols-outlined"> cancel </span>
      </button>
    </div>
  </div>

  <div class="card__bottom">
    <div class="card__progress">
      <div class="card__progress-active" style="width: {activeWidth};"></div>
    </div>
  </div>
</div>

<style>
  .card {
    padding: 1rem 2rem;
    border: 1px solid var(--color-border);
    border-radius: 8px;
    box-shadow: var(--box-shadow);
    background-color: var(--color-bg-secondary);
  }

  .card__top {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 1.5rem;
  }

  .card__timeLeft {
    font-size: 1.25rem;
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }

  .card__timeLeft span.active {
    color: var(--color-highlight-primary);
    animation: ring 4s 0.7s ease-in-out;
    animation-iteration-count: 5;
  }

  .card_actions {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 0.5rem;
  }

  .card__btn {
    background-color: transparent;
    color: var(--color-highlight-secondary);
    border: none;
    border-radius: 4px;
    padding: 0.25rem 1rem;
    cursor: pointer;
    transition: all ease-in-out 200ms;
  }

  .card__btn:hover {
    background-color: var(--color-bg-primary);
  }

  .card__progress,
  .card__progress-active {
    height: 8px;
    border-radius: 4px;
  }

  .card__progress {
    background-color: var(--color-bg-primary);
  }

  .card__progress-active {
    background-color: var(--color-highlight-secondary);
    transition: width 0.2s;
  }

  @keyframes ring {
    0% {
      transform: rotate(0);
    }
    1% {
      transform: rotate(30deg);
    }
    3% {
      transform: rotate(-28deg);
    }
    5% {
      transform: rotate(34deg);
    }
    7% {
      transform: rotate(-32deg);
    }
    9% {
      transform: rotate(30deg);
    }
    11% {
      transform: rotate(-28deg);
    }
    13% {
      transform: rotate(26deg);
    }
    15% {
      transform: rotate(-24deg);
    }
    17% {
      transform: rotate(22deg);
    }
    19% {
      transform: rotate(-20deg);
    }
    21% {
      transform: rotate(18deg);
    }
    23% {
      transform: rotate(-16deg);
    }
    25% {
      transform: rotate(14deg);
    }
    27% {
      transform: rotate(-12deg);
    }
    29% {
      transform: rotate(10deg);
    }
    31% {
      transform: rotate(-8deg);
    }
    33% {
      transform: rotate(6deg);
    }
    35% {
      transform: rotate(-4deg);
    }
    37% {
      transform: rotate(2deg);
    }
    39% {
      transform: rotate(-1deg);
    }
    41% {
      transform: rotate(1deg);
    }

    43% {
      transform: rotate(0);
    }
    100% {
      transform: rotate(0);
    }
  }
</style>
