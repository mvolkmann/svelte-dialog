<script>
  import {tick} from 'svelte';
  import Dialog from './Dialog.svelte';

  let dialog = null;
  let showDialog = false;

  async function openDialog() {
    showDialog = true;
    await tick(); // waits for dialog to be set
    dialog.showModal();
  }
</script>

<button on:click={openDialog}>Open Dialog</button>
<!-- #if is only necessary to implement the transition in
     Dialog.svelte because that only works if the <dialog>
     element is added to and removed from the DOM. -->
{#if showDialog}
  <Dialog bind:dialog on:close={() => showDialog = false} title="My Dialog Title">
    My dialog content is very, very long.<br>
    It will not wrap by default.
  </Dialog>
{/if}
