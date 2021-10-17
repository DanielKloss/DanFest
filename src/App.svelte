<script>
	import Current from "./Current.svelte";
	import History from "./History.svelte";

	let page = "history";
</script>

<main>
	<div class="header">
		<button on:click="{() => page = 'current'}" class="current">DANFEST</button>
		<div class="tabs">
			<p class="tab" on:click="{() => page = 'current'}" class:selected="{page === 'current'}">2021</p>
			<p class="tab" on:click="{() => page = 'history'}" class:selected="{page === 'history'}">HISTORY</p>
		</div>
	</div>

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

	.tabs {
		display: flex;
		align-self: flex-end;
		gap: 1rem;
	}

	.tab {
		background-color: #c9c9c9;
		font-family: 'Jost', sans-serif;
		margin-bottom: 0px;
		padding: 0.25rem 0.5rem;
		border-top-right-radius: 0.5rem;
		border-top-left-radius: 0.5rem;
		cursor: pointer;
	}

	.selected {
		background-color: white;
	}

	.header {
		display: flex;
		align-items: center;
		gap: 1rem;
		justify-content: space-between;
		list-style-type: none;
		background-color: #DE0000;
		padding: 1rem 0.5rem 0rem 1rem;
		margin: 0;
	}

	button {
		align-self: stretch;
		font-size: 4rem;
		font-family: carbonBlock;
		background-color: #DE0000;
		border:none;
		cursor: pointer;
	}
</style>