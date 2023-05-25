<script>
    import { now } from "svelte/internal";

    export let handleAddEvent;

	let eventName = '';
    let eventMessage = '';
    let eventDate = '';
    let repeat = false;
    let cycleEnded = false
    let sendNotif = true

    const clearInputs = () => {
        eventName = '';
        eventMessage = '';
        eventDate = '';
    };

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
			            NotificationUtils.showNotification('error', 'finito');
                        sendNotif = false
                    }
                    if(repeat){
                        timer = 20, minutes, seconds
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

<div class="countdown" style={cycleEnded ? "border-color: brown; " : "border-color: limegreen; "}>
    <h1 id="countdown">{countdown}</h1>
    <input type="checkbox" id="repeat" bind:value={repeat}>
    <label for="repeat">Repeat cycle?</label>
    <div style="margin-top: 1rem;">
        <button type="submit" on:click={() => start()}>Start</button>
        <button type="submit" on:click={() => reset()}>Reset</button>
    </div>
</div>

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
        background-color: limegreen;
        color:rgb(20, 20, 20);
		border-radius: 20px;
        height: 30px;
        border: 0;
        padding: 0 10px;
	}

    .itemInput textarea {
        grid-column: 1 / 3;
        min-height: 5rem;
		background-color: rgb(20, 20, 20);
		border: 2px solid limegreen;
		border-radius: 10px;
        color: white;
    }

	button {
		background-color: limegreen;
		border: 0;
		border-radius: 20px;
        color: black;
        place-self: center;
        grid-column: 1 / 3;
        padding: 8px 32px;
	}
    .countdown {
        padding: 20px 0;
        border-radius: 10px;
        margin: 20px 0;
        text-align: center;
        color: white;
        border: 2px solid limegreen;
    }
</style>