<script lang="ts">
  import { onMount } from "svelte";
  import Zoneinfo from "./components/Zoneinfo.svelte";
  let zones = [];

  onMount(async () => {
    console.log(process.env.BASE_URL);
    const res = await fetch(process.env.BASE_URL + "/home");
    zones = await res.json();
  });
</script>

<style>
</style>

<main>
  <h1>Welcome Home</h1>
  <ul>
    {#each zones as { ...zone }}
      <Zoneinfo {...zone} />
    {/each}
  </ul>
</main>
