<script>
	import TodoList from '@/lib/TodoList.svelte';
    import EventPropertyInputs from './lib/EventPropertyInputs.svelte';
	import { setContext } from 'svelte'

	let events = [];
	let endedEvents = []

	const deleteTopEvent = () => {
		if (events.length > 0) {
			console.log(events[0]);
			const topEid = events[0].id
			const eventName = events.filter(e => e.id = topEid)[0].name
			NotificationUtils.showNotification("event removed", `event ${eventName} removed`)
			endedEvents.push(events.find(event => event.id === topEid))
			events.splice(0,1);
			if (events[0]) { events[0].id = Math.floor(Date.now() * Math.random()) }
			events = events
			endedEvents = endedEvents
		}
	}

	setContext('events', { deleteTopEvent })

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

	const deleteEndedEvent = (id) => {
		const deletedEvent = endedEvents.find(event => event.id === id);
		clearTimeout(deletedEvent.reminderTimeout);
		endedEvents = endedEvents.filter(event => event.id !== id);
	}

</script>

<main>
	<EventPropertyInputs handleAddEvent="{addEvent}" />
	<TodoList events={events} endedEvents={endedEvents} handleDeleteEvent={deleteEvent} handleDeleteEndedEvent={deleteEndedEvent}/>
</main>

<style>
	main {
		background-color: lightblue;
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
