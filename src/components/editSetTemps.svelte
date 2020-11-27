<script lang="ts">
  import { onMount } from "svelte";
  import Modal from "./Modal.svelte";
  import SetTemp from "./setTemp.svelte";
  import SetTempForm from "./setTempForm.svelte";

  export var zone_num: number;
  export var closeTemps;
  var set_temps = [];
  var pickTime = false;

  const timePcikerOptions = {
    hasButtons: true,
    is24h: true,
  };

  onMount(async () => {
    const res = await fetch(
      process.env.BASE_URL + `/setTemps?zone_num=${zone_num}`
    );
    set_temps = await res.json();
  });

  function addSetTemp() {
    alert("test");
  }

  function closeTimeSet() {
    pickTime = false;
  }

  async function deleteTemp(id: string) {
    const res = await fetch(process.env.BASE_URL + `/setTemp?tempId=${id}`, {
      method: "DELETE",
    });
    if (res.ok) {
      set_temps = set_temps.filter((set_temp) => set_temp._id !== id);
    } else {
      console.log("Delete Temp Error");
    }
  }
</script>

<style>
</style>

<table>
  <!-- TODO - style this-->
  <th>Start Time</th>
  <th>Set Temp</th>
  <th>Remove</th>
  {#each set_temps as { ...set_temp }}
    <SetTemp {...set_temp} {deleteTemp} />
  {/each}
</table>
<button on:click={() => (pickTime = true)}>Add Set Temp</button>
<button type="button" on:click={closeTemps}>Close Modal</button>

{#if pickTime}
  <Modal on:close={() => (pickTime = false)}>
    <h1 slot="header">Add a Set Temp</h1>
    <p slot="content">
      <SetTempForm {zone_num} {closeTimeSet} />
    </p>
  </Modal>
{/if}
