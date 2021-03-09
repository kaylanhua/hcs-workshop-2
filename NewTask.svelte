<script>
	import { createEventDispatcher } from "svelte";
	
	let text = "";
	const dispatch = createEventDispatcher();
	
	function submit() {
		dispatch("newTask", text);
		text = ""; 
	}
</script>

<form on:submit|preventDefault={submit}>
	<input bind:value={text}> 
	<input type="submit">
</form>