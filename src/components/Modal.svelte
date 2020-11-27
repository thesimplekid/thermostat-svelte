<script lang="ts">
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();
  const close = () => dispatch("close");

  let modal;

  const handle_keydown = (e) => {
    if (e.key === "Escape") {
      close();
      return;
    }
  };
</script>

<style>
  div.modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;

    display: flex;
    justify-content: center;
    align-items: center;
  }
  div.backdrop {
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.4);
  }
  div.content-wrapper {
    z-index: 10;
    max-width: 70vw;
    border-radius: 0.3rem;
    background-color: white;
    overflow: hidden;
  }
  div.content {
    max-height: 100%;
    overflow: auto;
  }
</style>

<svelte:window on:keydown={handle_keydown} />
<div class="modal" bind:this={modal} on:keydown={handle_keydown}>
  <div class="backdrop" />

  <div class="content-wrapper">
    <slot name="header">
      <div>
        <h1>Your Modal Heading Goes Here...</h1>
      </div>
    </slot>

    <div class="content">
      <slot name="content" />
    </div>

    <!--  <slot name="footer"><button on:click={close}>close modal</button></slot> -->
  </div>
</div>
