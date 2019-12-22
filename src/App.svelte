<script>
  import Dialog from './Dialog.svelte';
  let myDialog = null;
  const openDialog = () => myDialog.showModal();
</script>

<button on:click={openDialog}>Open Dialog</button>
<Dialog bind:dialog={myDialog} title="My Dialog Title">
  My dialog content is very, very long.
  Will it wrap?
</Dialog>
