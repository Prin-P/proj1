<!--Adapted from https://svelte.dev/repl/885653f873284f7880490dcdd1200238?version=3.48.0-->
<script>
	export let dialog
</script>
<dialog bind:this={dialog} on:close>
	<slot/>
</dialog>
