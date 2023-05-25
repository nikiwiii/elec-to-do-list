<script>
<<<<<<< Updated upstream
=======
    import { now } from "svelte/internal";
	import { getContext } from 'svelte'
	const { deleteTopEvent } = getContext('events')

>>>>>>> Stashed changes
    export let handleAddEvent;

	let eventName = '';
    let eventMessage = '';
    let eventDate = '';

    const clearInputs = () => {
        eventName = '';
        eventMessage = '';
        eventDate = '';
    };

<<<<<<< Updated upstream
=======
    let countdown = "00:00"
    let timer = 10, minutes, seconds;
    let counting
    const originalTimer = timer
    const start = () => {
        counting = setInterval(function () {
            minutes = parseInt(timer / 60, 10)
            seconds = parseInt(timer % 60, 10);

            minutes = minutes < 10 ? "0" + minutes : minutes;
            seconds = seconds < 10 ? "0" + seconds : seconds;

            countdown = minutes + ":" + seconds;
            if(countdown != "00:00"){
                if (--timer < 0) {
                    cycleEnded = false
                    timer = duration;
                }
            }
            else {
                if(cycleEnded && repeat){
                    cycleEnded = false
                    timer = originalTimer
                    sendNotif = true
                }
                else {
                    cycleEnded = true
                    if(sendNotif){
				        deleteTopEvent()
                        sendNotif = false
                    }
                    if(repeat){
                        timer = 5, minutes, seconds
                    }
                }
            }
        }, 1000);
    }
    const reset = () => {
        cycleEnded = false
        countdown = "00:00"
        clearInterval(counting)
    }

>>>>>>> Stashed changes
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

<<<<<<< Updated upstream
=======
<div class="countdown" style={cycleEnded ? "border-color: grey; " : "border-color: limegreen; "}>
    <h1 id="countdown">{countdown}</h1>
    <input type="checkbox" id="repeat" bind:value={repeat}>
    <label for="repeat">Repeat cycle?</label>
    <div style="margin-top: 1rem;">
        <button type="submit" on:click={() => start()}>Start</button>
        <button type="submit" on:click={() => reset()}>Reset</button>
    </div>
</div>

>>>>>>> Stashed changes
<form class="itemInput" on:submit="{handleSubmit}">
	<input type="text" bind:value="{eventName}" name="event-name" placeholder="Event name" />
    <input type="datetime-local" bind:value="{eventDate}" name="event-date" />
    <textarea name="event-message" bind:value="{eventMessage}" placeholder="Event message" />
    <button type="submit">Add</button>
</form>

<style>
    * {
		font-family: Arial, Helvetica, sans-serif;
    }
	.itemInput {
		display: grid;
        margin: auto;
		margin-bottom: 1rem;
        grid-template-columns: 1fr 1fr;
        gap: 1rem;
        max-width: 600px;
	}

	.itemInput input {
		flex: 1;
<<<<<<< Updated upstream
		border: 2px solid lightcoral;
		border-radius: 0.25rem;
		background-color: white;

=======
        background-color: limegreen;
        color:rgb(20, 20, 20);
		border-radius: 1rem;
        height: 30px;
        border: 0;
        padding: 0 10px;
>>>>>>> Stashed changes
	}

    .itemInput textarea {
        grid-column: 1 / 3;
        min-height: 5rem;
<<<<<<< Updated upstream
=======
		background-color: rgb(20, 20, 20);
		border: 2px solid limegreen;
		border-radius: 1rem;
        color: white;
        resize: vertical;
        padding: 10px;
>>>>>>> Stashed changes
    }

	.itemInput button {
		background-color: lightcoral;
		border: 0;
<<<<<<< Updated upstream
		border-radius: 0.25rem;
		color: white;
=======
		border-radius: 1rem;
        color: black;
>>>>>>> Stashed changes
        place-self: center;
        grid-column: 1 / 3;
        padding: 0.5rem 2rem;
	}
<<<<<<< Updated upstream
=======
    .countdown {
        padding: 1rem 0;
        border-radius: 30px;
        text-align: center;
        color: white;
        width: fit-content;
        border: 2px solid limegreen;
        margin: auto;
        margin-bottom: 1rem;
        padding: 1rem;
    }
>>>>>>> Stashed changes
</style>