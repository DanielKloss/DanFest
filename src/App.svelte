<script>
	import Current from "./Current.svelte";
	import History from "./History.svelte";

    let year = new Date().getFullYear();
	let page = "current";
</script>

<main>
	<ul class="header">
		<button on:click="{() => page = 'current'}" class="current">DANFEST {year}</button>
		<img src="./history.svg" alt="" on:click="{() => page = 'history'}" class="history"/>
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
		padding: 0.25em 1em;
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
		width: 2em;
		cursor: pointer;
	}
</style>