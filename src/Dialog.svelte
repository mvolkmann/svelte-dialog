<!--
Dialog component creates a dialog that can have
an icon, a title, a close "X", and any content.
It is initially closed.

This uses the HTML `<dialog>` element.
Browser support this is not currently good, so a polyfill is required.
To get it, `npm install dialog-polyfill`.
Copy the files `dialog-polyfill.css` and `dialog-polyfill.js`
from `node_modules/dialog-polyfill/dist` to the `public` directory.
Add the following lines in the head section of `public/index.html`.

```html
    <link rel="stylesheet" href="dialog-polyfill.css" />
    <script src="dialog-polyfill.js"></script>
```

Parent components obtain a reference to the dialog element
by including the prop `bind:dialog={myDialog}`
where `myDialog` is a variable in the parent component.

To open the dialog as a modal, call `myDialog.showModal()`.
This prevents interaction with elements outside the dialog.

To open the dialog as a non-modal, call `myDialog.show()`.
This allows interaction with elements outside the dialog.

To close the dialog programatically, call `myDialog.close()`.
Parent components can listen for the dialog being closed
by the user by including the prop `on:close={handleClose}`
where `handleClose` is a function in the parent component.
-->
<script>
	import {createEventDispatcher, onMount} from 'svelte';
	
  // Boolean that determines whether a close "X" should be displayed.
  export let canClose = true;

  // Optional CSS class name to be added to the dialog element.
  export let className = '';

  // Parent components can use bind:dialog={myDialog} to get a
  // reference so they can call show(), showModal(), and close().
	export let dialog;

  // An optional icon to render in the header before the title.
	export let icon = undefined;

  // Title text to display in the dialog header.
	export let title;
	
	const dispatch = createEventDispatcher();
	
	$: classNames = 'dialog' + (className ? ' ' + className : '');
	
	onMount(() => dialogPolyfill.registerDialog(dialog));
	
	function close() {
    dispatch('close');
    dialog.close();
  }
</script>

<style>
	.body {
    padding: 10px;
  }

  button {
    margin: 0 5px;
  }
	
  .buttons {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 10px;
	}
	
  .close-btn {
    background-color: transparent;
    border: none;
    color: white;
    font-size: 24px;
    margin-right: 10px;
    outline: none;
    padding: 0;
  }

	dialog {
    /* These properties center the dialog in the browser window. */
    display: table;
    position: absolute;
    top: 50%;
    left: 50%;
    right: 50%;
    transform: translate(-50%, -50%);

    border: none;
    box-shadow: 0 0 10px darkgray;
    padding: 0;
	}
	
	/*
  .error-dialog .title {
    color: red;
  }
	*/

  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
		
    background-color: cornflowerblue;
    box-sizing: border-box;
    color: white;
    font-weight: bold;
    width: 100%;
  }

  section {
    margin: 0;
  }

  .title {
    display: flex;
    align-items: center;
    font-size: 18px;
    margin-right: 20px;
    padding: 10px;
  }

  ::backdrop,
  dialog + .backdrop {
    /* a transparent shade of gray */
    background-color: rgba(0, 0, 0, 0.2);
  }
</style>

<dialog bind:this={dialog} class={classNames} open={false}>
  <header>
    <div class="title">
      {#if icon}{icon}{/if}
      {title}
    </div>
    {#if canClose}
      <button class="close-btn" on:click={close}>
        &#x2716;
      </button>
    {/if}
  </header>
  <section class="body">
		<slot />
	</section>
</dialog>
