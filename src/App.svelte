<script lang="ts">
  import Timer from "./lib/components/Timer.svelte";
  import TimersList from "./lib/components/TimersList.svelte";
</script>

<main class="container">
  <Timer />
  <TimersList />
</main>

<style>
  .container {
    padding: 40px 30px 0 30px;
    margin: 0 auto;
    max-width: 870px;
    display: flex;
    flex-direction: column;
    gap: 3rem;
  }
</style>
