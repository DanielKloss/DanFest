<script>
	import Current from "./Current.svelte";
	import History from "./History.svelte";

    let year = new Date().getFullYear();
	let page = "current";
</script>

<main>
	<ul class="header">
		<button on:click="{() => page = 'current'}" >DANFEST {year}</button>
		<button on:click="{() => page = 'history'}" class="history">HISTORY</button>
	</ul>

	{#if page=="current"}
		<Current/>
	{:else}
		<History/>
	{/if}
</main>

<style>
	main {
		display: flex;
		flex-direction: column;
	}

	.header {
		display: flex;
		align-items: center;
		gap: 1em;
		justify-content: space-between;
		list-style-type: none;
		background-color: #DE0000;
		padding: 0.25em;
		margin: 0;
	}

	button {
		align-self: stretch;
		font-size: 4em;
		font-family: carbonBlock;
		background-color: #DE0000;
		border:none;
		cursor: pointer;
	}

	.history {
		font-size: 2em;
	}
</style>