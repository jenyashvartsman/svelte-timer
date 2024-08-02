<script lang="ts">
  import TimerCard from "./TimerCard.svelte";

  export let timers: number[] = [];
</script>

<div class="list">
  {#each timers as timer, i}
    <TimerCard {timer} />
  {/each}
</div>

<style>
  .list {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
</style>
