<script>
	import Item from '@/lib/Item.svelte';

	export let events;
	export let handleDeleteEvent;
</script>

<div>
	{#each events as event (event.id)}
		<div style:background={event.expired && 'rgba(255, 0, 0, 0.4)'}>
			<h2>{event.name}</h2>
			<p>{event.message}</p>
			<h4>{new Date(event.reminderTimestamp).toLocaleString()}</h4>
			{#if event.expired}
				<h5>Event expired</h5>
			{/if}
			<button on:click={() => handleDeleteEvent(event.id)}>Delete</button>
		</div>
		<!-- <Item title={item} index={index} onEdit={onEdit} onRemove={onRemove} /> -->
	{/each}
</div>

<style>
	div {
		border-top: 3px solid lightcoral;
	}
</style>