<script>
	import Item from '@/lib/Item.svelte';

	export let events;
	export let handleDeleteEvent;
</script>

<div style="display: flex; flex-direction: column">
	{#each events as event (event.id)}
		<div class="yuh" style:background={event.expired && 'brown'}>
			{#if event.expired}
				<h5>Event expired</h5>
			{/if}
			<div>
				<p>Event name: </p>
				<h2>{event.name}</h2>
				<p>Event message: </p>
				<h2>{event.message}</h2>
			</div>
			<div style:background={event.expired && 'brown'}>
				<p>Made on: </p>
				<h2>{new Date(event.reminderTimestamp).toLocaleString()}</h2>
				<button on:click={() => handleDeleteEvent(event.id)}>Delete</button>
			</div>
		</div>
		<!-- <Item title={item} index={index} onEdit={onEdit} onRemove={onRemove} /> -->
	{/each}
</div>

<style>
	.yuh {
		background-color: limegreen;
		border-radius: 10px;
		color: white;
		display: flex;
		width: min-content;
		align-self: center;
		margin-top: 20px
	}
	.yuh div {
		background-color: rgb(20, 20, 20);
		margin: 2px;
		border-radius: 10px;
		width: 150px;
	}
	.yuh div:nth-of-type(2) {
		background-color: limegreen;
		color: rgb(20, 20, 20)
	}
	.yuh div *:not(button) {
		margin: 10px;
		font-size: 24px;
	}
	.yuh div p {
		font-size: 15px;
		margin: 10px;
	}
	button {
		background-color: rgb(20, 20, 20);
		border: 0;
		border-radius: 20px;
    	width: -webkit-fill-available;
		height: 30px;
		margin: 10px;
		color: limegreen;
	}
	* {
		font-weight: normal;
	}
</style>