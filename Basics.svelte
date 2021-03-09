<script>
	let name = "Will";
	
	// Data binding
	let src = "https://i.pinimg.com/originals/94/dd/e1/94dde1ac061851a9bd525755457f26f0.jpg";
	
</script>

<div class="outerdiv">
	<h1> Hello, {name + " " + "Cooper"}! </h1>
	<p> This is a paragraph. </p>
	<p> This is a second <strong>paragraph</strong></p>
</div>
	
<input bind:value={name}>

{#each [...Array(5)] as i}
<img {src} alt="nice pink picture" width="200px">
{/each}

<style>
	.outerdiv {
		border: 1px solid black;
	}
	h1 {
		color: pink;
		font-size: 3rem;
		font-weight: 300;
		text-decoration: underline;
		text-align: center;
	}
</style>