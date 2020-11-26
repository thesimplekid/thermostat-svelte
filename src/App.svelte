<script lang="ts">
  import { onMount } from "svelte";
  import Zoneinfo from "./components/Zoneinfo.svelte";
  import Modal from "./components/Modal.svelte";
  import AddZone from "./components/addZone.svelte";

  let zones = [];
  export let showModal = false;

  onMount(async () => {
    const res = await fetch(process.env.BASE_URL + "/home");
    zones = await res.json();
  });

  async function handleSubmitted(event) {
    const zoneInfo = event.detail.zoneInfo;

    const res = await fetch(process.env.BASE_URL + "/addZone", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(zoneInfo),
    });

    if (res.ok) {
      showModal = false;
      location.reload();
      return false;
    } else {
      alert("Zone Settings not saved");
    }
  }
</script>

<style>
</style>

<h1>Welcome Home</h1>

<ul>
  {#each zones as { ...zone }}
    <Zoneinfo {...zone} />
  {/each}
</ul>

<button on:click={() => (showModal = true)}>Add Zone</button>

{#if showModal}
  <Modal on:close={() => (showModal = false)}>
    <h1 slot="header">Add a Zone</h1>
    <p slot="content">
      <AddZone on:submitted={handleSubmitted} />
    </p>
  </Modal>
{/if}
