<script lang="ts">
  import { onMount } from "svelte";
  import SetTemp from "./setTemp.svelte";

  export var zone_num: number;
  var set_temps = [];

  onMount(async () => {
    const res = await fetch(
      process.env.BASE_URL + `/setTemps?zone_num=${zone_num}`
    );
    set_temps = await res.json();
  });
</script>

<style>
</style>

<table>
  <!-- TODO - style this-->
  <th>Start Time</th>
  <th>Set Temp</th>
  <th>Remove</th>
  {#each set_temps as { ...set_temp }}
    <SetTemp {...set_temp} />
  {/each}
  <!-- TODO - add set temp -->
</table>
