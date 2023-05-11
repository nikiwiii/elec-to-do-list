<script>
    export let handleAddEvent;

	let eventName = '';
    let eventMessage = '';
    let eventDate = '';

    const clearInputs = () => {
        eventName = '';
        eventMessage = '';
        eventDate = '';
    };

    const handleSubmit = (event) => {
        event.preventDefault();

        if (!eventName || !eventDate) {
            return NotificationUtils.showDialog(
                'error',
                'Invalid data',
                'Event name and event date must be filled'
            );
        }

        const reminderTimestamp = Date.parse(eventDate);

        if (reminderTimestamp <= Date.now()) {
            return NotificationUtils.showDialog(
                'error',
                'Invalid data',
                'Event date must be in the future'
            );
        }

        handleAddEvent({
            name: eventName,
            message: eventMessage,
            reminderTimestamp
        });

        clearInputs();
    };
</script>

<form class="itemInput" on:submit="{handleSubmit}">
	<input type="text" bind:value="{eventName}" name="event-name" placeholder="Event name" />
    <input type="datetime-local" bind:value="{eventDate}" name="event-date" />
    <textarea name="event-message" bind:value="{eventMessage}" />
    <button type="submit">Add</button>
</form>

<style>
	.itemInput {
		display: grid;
		margin-bottom: 2rem;
        grid-template-columns: 1fr 1fr;
        gap: 1rem;
	}

	.itemInput input {
		flex: 1;
		border: 2px solid lightcoral;
		border-radius: 0.25rem;
		background-color: white;

	}

    .itemInput textarea {
        grid-column: 1 / 3;
        min-height: 5rem;
    }

	.itemInput button {
		background-color: lightcoral;
		border: 0;
		border-radius: 0.25rem;
		color: white;
        place-self: center;
        grid-column: 1 / 3;
        padding: 0.5rem 2rem;
	}
</style>