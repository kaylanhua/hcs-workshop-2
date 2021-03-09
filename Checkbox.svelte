<script>
	export let value;
</script>

<button on:click>
	{value ? "🤢" : "💋"}
</button>

<style>
	button {
		width: 32px;
		height: 32px;
		padding: 0px;
		margin: 0px;
		margin-right: 10px;
	}
</style>