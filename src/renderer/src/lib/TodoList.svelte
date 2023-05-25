<script>
	import Item from '@/lib/Item.svelte';

	export let events;
	export let endedEvents
	export let handleDeleteEvent;
	export let handleDeleteEndedEvent;
</script>

<div class="scroll-area">
	<div style="display: flex; flex-direction: row">
		{#each endedEvents as event (event.id)}
		<div class="nah">
			<div>
				<p>Event name: </p>
				<h2><s>{event.name}</s></h2>
				<p>Event message: </p>
				<h2><s>{event.message}</s></h2>
			</div>
			<div>
				<p>Made on: </p>
				<h2><s>{new Date(event.reminderTimestamp).toLocaleString()}</s></h2>
				<button on:click={() => handleDeleteEndedEvent(event.id)}>Delete</button>
			</div>
			<!-- <Item title={item} index={index} onEdit={onEdit} onRemove={onRemove} /> -->
		</div>
		{/each}
		{#each events as event (event.id)}
		<div class="yuh" style:background={event.expired && 'grey'}>
			{#if event.expired}
				<h5>&nbsp; E X P I R E D</h5>
			{/if}
			<div>
				<p>Event name: </p>
				<h2>{event.name}</h2>
				<p>Event message: </p>
				<h2>{event.message}</h2>
			</div>
			<div style:background={event.expired && 'grey'}>
				<p>Made on: </p>
				<h2>{new Date(event.reminderTimestamp).toLocaleString()}</h2>
				<button on:click={() => handleDeleteEvent(event.id)}>Delete</button>
			</div>
			<!-- <Item title={item} index={index} onEdit={onEdit} onRemove={onRemove} /> -->
		</div>
		{/each}
	</div>
</div>

<style>
	.yuh, .nah {
		background-color: limegreen;
		border-radius: 1rem;
		color: white;
		display: flex;
		width: min-content;
		align-self: center;
		margin-right: 1rem;
		margin-bottom: 1rem
	}
	.nah {
		background-color: grey;
	}
	.yuh div, .nah div {
		background-color: rgb(20, 20, 20);
		margin: 2px;
		border-radius: 1rem;
		width: 150px;
	}
	.yuh div:nth-of-type(2) {
		background-color: limegreen;
		color: rgb(20, 20, 20)
	}
	.nah div:nth-last-of-type(2) {
		background-color: grey;
		color: rgb(20, 20, 20)
	}
	.yuh div *:not(button), .nah div *:not(button) {
		margin: 10px;
		font-size: 24px;
	}
	.yuh div p, .nah div p {
		font-size: 15px;
		margin: 10px;
	}
	button {
		background-color: rgb(20, 20, 20);
		border: 0;
		border-radius: 1rem;
    	width: -webkit-fill-available;
		height: 30px;
		margin: 10px;
		color: limegreen;
	}
	* {
		font-weight: normal;
	}
	h5 {
		width: min-content; 
		font-size: 15px; 
		margin: 0; 
		color: black; 
		font-weight: bold; 
		text-align: center
	}
	.scroll-area {
		width: 75%; 
		max-width: 600px;
		overflow: hidden; 
		overflow-x: scroll;
        margin: auto;
	}
	::-webkit-scrollbar {
		width: 1rem
	}
	::-webkit-scrollbar-track {
		background-color: rgb(40, 40, 40);
		border-radius: 1rem;
	}
	::-webkit-scrollbar-thumb {
		background-color: limegreen;
		border-radius: 1rem;
	}
</style>