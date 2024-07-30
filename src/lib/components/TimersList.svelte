<script lang="ts">
  import type { TimerDto } from "../dto/timer.dto";
  import TimerCard from "./TimerCard.svelte";

  const timers: number[] = [50, 85, 90];
</script>

<div class="list">
  {#each timers as timer}
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
