<script>
	import { fade, slide } from "svelte/transition";
	
	import Checkbox from "./Checkbox.svelte";
	import Delete from "./Delete.svelte";
	import NewTask from "./NewTask.svelte";
	
	let tasks = null; 
	let mode = "all";
	
	$: console.log(mode);
	
	$: filteredTasks = tasks?.filter((task) => {
		if (mode === "all") 
			return true;
		if (mode === "active")
			return !task.completed;
		if (mode == "completed")
			return task.completed;
	});
	
	fetch("https://api.mocki.io/v1/7ea36673")
		.then((resp) => resp.json())
		.then((data) => tasks = data);
	
	$: console.log(tasks);
	
	function toggle(task) {
		task.completed = !task.completed;
		tasks = tasks;
	}
	
	function remove(task) {
		tasks = tasks.filter((t) => task !== t);
	}
	
	function add(event) {
		tasks = [...tasks, { text: event.detail, completed: false }];
	}
	
</script>

<main>
	<h2>HCS TODO LIST</h2>
	{#if tasks === null}
	<p>
		Your tasks are loading...
	</p>
	{:else}
	<div class="controls">
		<button class:selected={mode === "all"} on:click={() => mode = "all"}>All</button>
		<button class:selected={mode === "active"} on:click={() => mode = "active"}>Active</button>
		<button class:selected={mode === "completed"} on:click={() => mode = "completed"}>Completed</button>
	</div>
	<ul class="tasks">
		{#each filteredTasks as task (task)}
		<li transition:slide>
			<Checkbox on:click={() => toggle(task)} value={task.completed} />
			<span>{task.text.toLowerCase()}</span>
			<Delete on:click={() => remove(task)}/>
		</li>
		{/each}
	</ul>
			
	<NewTask on:newTask={add} />
	{/if}

</main>

<style>
	main {
		width: 480px;
		margin: 0 auto;
		display: flex;
		flex-direction: column;
		align-items: center;
	}
	
	h2 {
		color: purple;
		font-size: 2rem;
		font-weight: 300;
		margin-bottom: 1rem;
	}
	
	.tasks {
		width: 100%;
		border: 2px solid black;
		list-style-type: none;
		padding: 0;
	}
	
	.tasks > li {
		padding: 8px 12px;
		display: flex;
		align-items: center;
		transition: background 0.5s;
	}
	
	.tasks > li:hover {
		background: rgba(0, 0, 255, 0.05);
	}
	
	.tasks > li:not(:first-child) {
		border-top: 1px solid lightgrey;
	}
	
/* 	.controls {
		margin-bottom: 0.5rem;
	} */
	
	.controls > button.selected {
		font-weight: bold;
	}
	
	</style>
