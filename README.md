# svelte-dialog

This demonstrates implementing a Svelte Dialog component
that uses the HTML `<dialog>` element.

## Steps to run

1. `npm install`
2. `npm run dev`
3. Click the "Open Dialog" button.
4. Click the "X" in the upper-right to close the dialog.

## Steps to use

The `Dialog` component can have an icon, a title, a close "X",
and any content.  It is initially closed.

The `Dialog` component uses the HTML `<dialog>` element.
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

