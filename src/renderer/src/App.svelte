<script>
	import TodoList from '@/lib/TodoList.svelte';
    import EventPropertyInputs from './lib/EventPropertyInputs.svelte';

	let events = [];

	const addEvent = (event) => {
		event.id = Math.floor(Date.now() * Math.random());

		const timeBetween = event.reminderTimestamp - Date.now();

		event.reminderTimeout = setTimeout(() => {
			NotificationUtils.showNotification(event.name, event.message);
			event.expired = true;
			events = events;
		}, timeBetween);

		events = [...events, event];
	};

	const deleteEvent = (id) => {
		const deletedEvent = events.find(event => event.id === id);
		clearTimeout(deletedEvent.reminderTimeout);
		events = events.filter(event => event.id !== id);
	}
</script>

<main>
	<EventPropertyInputs handleAddEvent="{addEvent}" />
	<TodoList events={events} handleDeleteEvent={deleteEvent} />
</main>

<style>
	* {
		font-family: Arial, Helvetica, sans-serif;
	}
	main {
		background-color: rgb(20, 20, 20);
		margin: 0;
		padding: 15px;
		min-height: calc(100vh - 30px);
	}
	:global(body) {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}
</style>
