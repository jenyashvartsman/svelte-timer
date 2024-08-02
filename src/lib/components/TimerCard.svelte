<script lang="ts">
  export let timer: number;

  let timeLeft: number;
  let activeWidth: string;

  $: {
    timeLeft = timer;
    activeWidth = `${((timeLeft / timer) * 100).toFixed(2)}%`;
  }

  $: format = (): string => {
    const minutes = Math.floor(timeLeft / 60);
    const seconds = timeLeft % 60;
    return `${minutes > 9 ? minutes : "0" + minutes} minutes ${seconds > 9 ? seconds : "0" + seconds} seconds`;
  };
</script>

<div class="card">
  <div class="card__top">
    <h3 class="card__timeLeft">
      <span class="material-symbols-outlined"> notifications </span>
      <span>{format()}</span>
    </h3>
    <div class="card_actions">
      <button class="card__btn">
        <span class="material-symbols-outlined"> pause_circle </span>
      </button>

      <button class="card__btn">
        <span class="material-symbols-outlined"> play_circle </span>
      </button>

      <button class="card__btn">
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
  }
</style>
