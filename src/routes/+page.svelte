<script>
	import Counter from './Counter.svelte';
	let days = 0;
	let hours = 0;
	let minutes = 0;

	let shownDays = 0;
	let shownHours = 0;
	let shownMinutes = 0;

	function calculateThings() {
		console.log("I'm calculating things");
		shownDays = days;
		shownHours = hours;
		shownMinutes = minutes;
	}

</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<h1>
		<span class="welcome">
			How much time do you have?
		</span>
	</h1>
	<section class="counters">
		<Counter counterName = {"Days"} bind:value={days}/>
		<Counter counterName = {"Hours"} bind:value={hours}/>
		<Counter counterName = {"Minutes"} bind:value={minutes}/>
	</section>

	{#if shownDays > 0 || shownHours > 0 || shownMinutes > 0}
		<span>
			Your Input {shownDays} {shownHours} {shownMinutes}
		</span>
	{/if}

	<button class= "btn-grad" on:click={()=>calculateThings()}>
		Lemme Calculate
	</button>

</section>

<style>

	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		height: max-content;
		align-items: center;
		flex: 0.6;
	}

	section.counters {
		flex-direction: row;
	}

	h1 {
		width: 100%;
	}

	.welcome {
		display: block;
		position: relative;
		width: 100%;
		height: 0;
	}
         
	.btn-grad {
		background-image: linear-gradient(to right, #4776E6 0%, #8E54E9  51%, #4776E6  100%);
		margin: 10px;
		padding: 15px 45px;
		text-align: center;
		text-transform: uppercase;
		transition: 0.5s;
		background-size: 200% auto;
		color: white;            
		box-shadow: 0 0 20px #eee;
		border-radius: 10px;
		display: block;
		}

		.btn-grad:hover {
		background-position: right center; /* change the direction of the change here */
		color: #fff;
		text-decoration: none;
		cursor:pointer;
		}
		
</style>
