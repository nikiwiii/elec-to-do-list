<script>
	import Item from '@/lib/Item.svelte';

	export let items = [];
	export let onRemove;
	export let onEdit;
</script>

<div>
	{#each items as item, index}
		<Item title={item} index={index} onEdit={onEdit} onRemove={onRemove} />
	{/each}
</div>

<style>
	div {
		border-top: 3px solid lightcoral;
	}
</style>