<script lang="ts">
  import { onMount } from "svelte";
  import Zoneinfo from "./components/Zoneinfo.svelte";
  import Modal from "./Modal.svelte";

  let zones = [];
  let showModal = false;

  onMount(async () => {
    const res = await fetch(process.env.BASE_URL + "/home");
    zones = await res.json();
  });
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
    <h1 slot="header">Tester header info</h1>
    <h1 slot="content">content stuff</h1>
  </Modal>
{/if}
