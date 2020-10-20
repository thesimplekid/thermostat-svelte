<script lang="ts">
  import { onMount } from "svelte";
  import Zoneinfo from "./components/Zoneinfo.svelte";
  let zones = [];

  onMount(async () => {
    const res = await fetch("http://10.30.30.92:3000/temperatures/home");
    zones = await res.json();
  });
</script>

<style>
</style>

<main>
  <ul>
    {#each zones as { ...zone }}
      <Zoneinfo {...zone} />
    {/each}
  </ul>
</main>
