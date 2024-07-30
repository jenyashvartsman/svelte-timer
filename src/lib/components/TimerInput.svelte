<script lang="ts">
  let value: number = 0;
</script>

<div class="input">
  <button class="input__btn">
    <span class="material-symbols-outlined"> add </span>
  </button>

  <span class="input__value">{value}</span>

  <button class="input__btn">
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

  .input__btn:hover {
    background-color: transparent;
    color: var(--color-highlight-primary);
  }
</style>
