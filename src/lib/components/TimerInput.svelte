<script lang="ts">
  import { createEventDispatcher } from "svelte";

  export let value: number = 0;
  export let valueType: "M" | "S";
  export let addDisabled = false;
  export let subtractDisabled = false;

  const dispatch = createEventDispatcher();

  $: format = (): string => {
    const valueStr = value > 9 ? `${value}` : `0${value}`;
    return `${valueStr}${valueType}`;
  };

  function handleClick(addToValue: number): void {
    dispatch("valueChanged", addToValue);
  }
</script>

<div class="input">
  <button
    class="input__btn"
    on:click={() => handleClick(1)}
    disabled={addDisabled}
  >
    <span class="material-symbols-outlined"> add </span>
  </button>

  <span class="input__value">{format()}</span>

  <button
    class="input__btn"
    on:click={() => handleClick(-1)}
    disabled={subtractDisabled}
  >
    <span class="material-symbols-outlined"> remove </span>
  </button>
</div>

<style>
  .input {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    gap: 0.5rem;
  }

  .input__btn {
    background-color: var(--color-highlight-primary);
    border: 1px solid var(--color-highlight-primary);
    border-radius: 4px;
    height: 32px;
    width: 32px;
    cursor: pointer;
    transition: all ease-in-out 200ms;
  }

  .input__btn:hover:not(:disabled) {
    background-color: transparent;
    color: var(--color-highlight-primary);
  }

  .input__btn:disabled {
    opacity: 0.9;
    cursor: not-allowed;
  }
</style>
