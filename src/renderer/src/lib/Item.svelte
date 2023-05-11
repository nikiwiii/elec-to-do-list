<script>
	export let title;
	export let index;

	export let onEdit;
	export let onRemove;
	let editedTitle = title;
	let isEditing = false;

	function confirmEdit() {
		if (editedTitle != "") {
			onEdit(index, editedTitle);
			isEditing = false;
		}
	}
	function cancelEdit() {
		isEditing = false;
		editedTitle = title;
	}
	window.addEventListener("keydown", (e) => {
		if(!isEditing) return;
		switch(e.key){
			case "Enter":
				confirmEdit();
				break;
			case "Escape":
				cancelEdit();
				break;
			default:
				break;
		}
	});
</script>

<div class="wrapper">
	{#if !isEditing}
		<p>{title}</p>
		<div class="button-container">
			<button
				on:click={() => {
					isEditing = true;
				}}>Edit</button
			>
			<button
				on:click={() => {
					onRemove(index);
				}}>Remove</button
			>
		</div>
	{:else}
		<input type="text" placeholder="Title..." bind:value={editedTitle} />
		<div class="button-container">
			<button
				class="button-save"
				on:click={confirmEdit}>
				Save
			</button>
			<button 
				class="button-cancel"
				on:click={cancelEdit}>
				Cancel
			</button>
		</div>
	{/if}
</div>

<style>
	.button-save {
		background-color: lime;
	}
	.wrapper {
		height: 2rem;
		background-color: lightblue;
		border-bottom: 3px solid lightcoral;
		display: flex;
		justify-content: space-between;
	}
	.button-container {
		height: 100%;
		display: flex;
		align-items: center;
	}

	button {
		min-width: fit-content;
		max-width: 250px;
		width: 10vw;
		margin: 5px;
		margin-left: auto;
		background-color: lightcoral;
		border: 0;
		height: 80%;
		cursor: pointer;
	}
</style>
