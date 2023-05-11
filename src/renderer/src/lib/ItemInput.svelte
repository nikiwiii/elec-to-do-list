<script>
	export let onAdd;

	let item = '';

	function addItem() {
		if (item) {
			onAdd(item);
			item = '';
		}
	}

	function handleKeyDown(event) {
		if (event.key === 'Enter') {
			addItem();
		}
	}
</script>

<div class="itemInput">
	<input type="text" bind:value={item} placeholder="Add a new item" on:keydown={handleKeyDown} />
	<button on:click={addItem}>Add</button>
</div>

<style>
	.itemInput {
		display: flex;
		height: 2rem;
		margin-bottom: 2rem;
	}

	.itemInput input {
		flex: 1;
		border: 2px solid lightcoral;
		border-radius: 0.25rem;
		background-color: white;

	}

	.itemInput button {
		margin-left: 1em;
		background-color: lightcoral;
		border: 0;
		border-radius: 0.25rem;
		color: white;
	}
</style>